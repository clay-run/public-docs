---
title: Connect Clay to Amazon Bedrock
description: Run Use AI and Claygent on models in your own Amazon Bedrock account. Clay signs in with short-lived AWS credentials through OIDC federation, so there is no access key to share or rotate. Available on all Enterprise plans.
---

# Connect Clay to Amazon Bedrock

Run Use AI and Claygent on models in your own Amazon Bedrock account. Clay signs in to AWS with short-lived (two-hour) credentials through OpenID Connect (OIDC) federation, so there is no AWS access key to share, store, or rotate.

**Availability:** Amazon Bedrock is available on all Enterprise plans.

**Billing with an Amazon Bedrock account:** When a Use AI or Claygent column uses your Amazon Bedrock connection, AWS bills model usage to your AWS account. Clay does not charge Data Credits for it. The action cost (1 per AI run) is still consumed from your Clay balance, the same as with any other own-API-key account.

## Choose a Bedrock endpoint

When you create the connection, pick one of two endpoints:

-   **Runtime endpoint** (default, recommended): Uses Bedrock's cross-region inference, so supported models are available from more regions. Turn on **US-only inference** to keep requests in the US. This requires the **AWS region** to be `us-east-1`, `us-east-2`, `us-west-1`, or `us-west-2`.
-   **Mantle endpoint**: Sends requests only to the AWS region you choose, with no cross-region inference. The models available depend on that region. Choose Mantle if you need a model only Mantle offers, or if requests must stay in one region.

## Supported models

-   Runtime and Mantle endpoints: Claude Opus 5.5, Claude Opus 5, Claude Opus 4.8, Claude Opus 4.7, Claude Sonnet 5.5, Claude Sonnet 5, Claude Haiku 5.5, Claude Haiku 4.5, GPT-5.6 Sol, GPT-5.6 Terra, and GPT-5.6 Luna.
-   Mantle endpoint only: GPT-5.5 and GPT-5.4.

Mantle availability for each model also depends on your AWS region. See AWS's [model regional availability](https://docs.aws.amazon.com/bedrock/latest/userguide/models-region-compatibility.html) page. You can't use other models with an Amazon Bedrock connection.

## Before you connect Amazon Bedrock

You need:

-   A Clay Enterprise plan.
-   AWS permissions to create IAM identity providers, roles, and policies.
-   Model access enabled in the Bedrock console for the models you'll use.

## Connecting Amazon Bedrock to Clay

1.  In Clay, go to **Settings** → **Connections**, click **Create**, and choose **Amazon Bedrock**. (You can also click **Add account** from the **Account** dropdown in a Use AI or Claygent column.)
2.  Pick **Runtime endpoint** or **Mantle endpoint**.
3.  Copy the two values Clay shows: the **Issuer** (`https://identity.clay.com`) and the **Connection subject** (formatted like `workspace:12345:connection:oidc_…`). The connection subject is unique to this connection and stays the same when you reconnect. The setup window lasts seven days. If it lapses, click **Renew authorization**.
4.  In AWS IAM, go to **Identity providers** → **Add provider** → **OpenID Connect**. Set **Provider URL** to the Issuer and set **Audience** to a value of your choice, such as `sts.amazonaws.com`. Note the audience for step 8. Skip this step if the AWS account already has a Clay identity provider (for example, from an [Amazon Redshift connection](connect-clay-to-amazon-redshift.md)).
5.  Create an IAM role of type **Web identity** using that provider and audience. In the role's trust policy, allow `sts:AssumeRoleWithWebIdentity` with `StringEquals` conditions on the audience (`identity.clay.com:aud`) and the full connection subject (`identity.clay.com:sub`). Use the full connection subject — never a wildcard.
6.  Set the role's **Maximum session duration** to **2 hours** (7200 seconds). New IAM roles default to 1 hour, and Clay requires 2-hour sessions for Amazon Bedrock.
7.  Attach a permissions policy for your endpoint:
    -   Runtime endpoint: allow `bedrock:InvokeModel`, `bedrock:InvokeModelWithResponseStream`, and `bedrock:GetInferenceProfile` on the inference profiles and foundation models you'll use.
    -   Mantle endpoint: allow `bedrock-mantle:CreateInference`.
8.  Back in Clay, fill in **IAM role ARN**, **Audience** (the exact audience from step 4), **AWS region**, and, for the Runtime endpoint only, the optional **US-only inference** toggle. Click save.

Clay confirms it can assume the role. The Amazon Bedrock connection then appears in the **Account** dropdown for supported models in [Use AI](use-ai-integration-overview.md) and Claygent.

## Troubleshooting the Amazon Bedrock connection

-   **"The role's maximum session duration is under 2 hours.":** Set the IAM role's maximum session duration to at least 2 hours (7200 seconds), then reconnect.
-   **"AWS STS rejected the federated assume-role" on save:** The provider URL, audience, or connection subject in AWS doesn't exactly match the values Clay shows.
-   **Access denied when a column runs:** The IAM role is missing permissions for your endpoint, or model access isn't enabled in Bedrock for that model.
