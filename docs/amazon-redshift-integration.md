---
title: Amazon Redshift integration
description: Connect Clay to your Amazon Redshift Serverless workgroup or provisioned cluster with short-lived AWS credentials and import records into Audiences. Available to select Enterprise workspaces, currently in alpha.
---

# Amazon Redshift integration

Connect Clay to your own Amazon Redshift warehouse and import records from it into Clay Audiences.

**Availability:** The Amazon Redshift integration is currently in alpha and available to an initial set of Enterprise customers. If you don't see Amazon Redshift as a connection option in your workspace, contact your Clay account team to ask about enrolling your workspace.

**What the Amazon Redshift integration supports:** Amazon Redshift can only be used as an Audiences source — to import records from Redshift into Audiences. Amazon Redshift workflow actions and table actions (such as inserting, looking up, or updating rows) aren't available.

Clay connects to your Amazon Redshift Serverless workgroup or provisioned cluster using short-lived AWS credentials obtained through OpenID Connect (OIDC) federation, so you never share a Redshift password or AWS access key, and there is nothing to rotate. Clay runs queries through the Amazon Redshift Data API, so you don't need to open network access or allowlist Clay's IP addresses.

## Before you connect Amazon Redshift

To connect Amazon Redshift to Clay, you need:

-   Amazon Redshift enabled in your Clay workspace (see **Availability** above).
-   AWS permissions to create IAM identity providers, roles, and policies.
-   A Redshift user who can run `GRANT` on the schemas and tables Clay should read.

## Connecting Amazon Redshift to Clay

1.  In Clay, go to **Settings** → **Connections**, click **Create**, and choose **Amazon Redshift**.
2.  Copy the two values Clay shows: the **Issuer** (`https://identity.clay.com`) and the **Connection subject** (formatted like `workspace:12345:connection:oidc_…`). The connection subject is unique to this connection and stays the same when you reconnect. The setup window lasts seven days — if it lapses, click **Renew authorization**.
3.  In AWS IAM, go to **Identity providers** → **Add provider** → **OpenID Connect**. Set **Provider URL** to the Issuer from Clay and set **Audience** to a value of your choice, such as `sts.amazonaws.com`. Note the audience for step 6. Skip this step if the AWS account already has a Clay identity provider (for example, from an Amazon Bedrock connection).
4.  Create an IAM role of type **Web identity** using that provider and audience. In the role's trust policy, allow `sts:AssumeRoleWithWebIdentity` with `StringEquals` conditions on the audience (`identity.clay.com:aud`) and the full connection subject (`identity.clay.com:sub`). Use the full connection subject — never a wildcard.
5.  Attach a permissions policy that lets the role run statements on your warehouse through the Redshift Data API and read its own statement results:
    -   **Redshift Serverless:** allow `redshift-serverless:GetCredentials`, `redshift-data:ExecuteStatement`, and `redshift-data:BatchExecuteStatement` on the workgroup, plus `redshift-data:DescribeStatement`, `redshift-data:GetStatementResult`, `redshift-data:CancelStatement`, and `redshift-data:ListStatements`.
    -   **Provisioned cluster:** allow `redshift-data:ExecuteStatement` and `redshift-data:BatchExecuteStatement` on the cluster, `redshift:GetClusterCredentialsWithIAM` on the database, plus the same four statement-result actions.
6.  Back in Clay, fill in the connection form and save:
    -   **IAM role ARN** — the ARN of the role from step 4.
    -   **Audience** — the exact audience from step 3.
    -   **AWS region** — the region of your workgroup or cluster, for example `us-east-1`.
    -   **Database** — the database to query, for example `dev`.
    -   **Serverless workgroup name** (for Redshift Serverless) or **Provisioned cluster identifier** (for a provisioned cluster). Fill in the one that matches your warehouse type.
7.  On save, Clay assumes the role and runs a test query (`SELECT current_user`) to confirm it can reach your warehouse. Clay can't read your tables yet — step 8 grants that access.
8.  Grant read access to Clay's Redshift database user. Clay connects as the database user `IAMR:<role name>` (for example, `IAMR:ClayRedshiftAccess`), which Redshift creates the first time the role connects in step 7. Grant it `USAGE` on each schema and `SELECT` on the tables Clay should read:

    ```sql
    GRANT USAGE ON SCHEMA analytics TO "IAMR:ClayRedshiftAccess";
    GRANT SELECT ON ALL TABLES IN SCHEMA analytics TO "IAMR:ClayRedshiftAccess";
    ```

**Amazon Redshift access is read-only.** Clay only needs `SELECT` permission. Clay rejects any Redshift query that isn't a read-only `SELECT` or `WITH` statement.

## Importing Amazon Redshift data into Audiences

After you connect Amazon Redshift, you can import records from it into Audiences:

1.  In Audiences, click **Add data** → **Add Source** and select **Amazon Redshift**.
2.  Choose your Amazon Redshift account, name the import, choose **Companies** or **People**, and enter a SQL `SELECT` query that defines which records to import.
3.  After the import is created, open its settings and choose a **Unique identifier** — a column that is unique and non-null for every record. Clay uses it to decide whether an incoming row creates a new Audiences record or updates an existing one.
4.  (Optional) Choose a **Timestamp field** — a `TIMESTAMP` column — for incremental syncing.
5.  Map your Redshift columns to Audience fields.

**Amazon Redshift sync timing:** On Enterprise plans, when a **Timestamp field** is configured, the incremental sync runs every **15 minutes** and imports only new or changed rows. Without a timestamp field, the sync runs every **12 hours**. A full sync runs every **7 days** to re-read all records and reconcile deleted records.

## Troubleshooting the Amazon Redshift connection

-   **"AWS STS rejected the federated assume-role" on save:** the provider URL, audience, or connection subject in AWS doesn't exactly match the values Clay shows.
-   **Permission denied for a schema or table when Clay queries Redshift:** run the `GRANT` statements in step 8 for that schema, using the `IAMR:<role name>` user.
-   **Amazon Redshift doesn't appear in Settings → Connections:** the integration isn't enabled for your workspace yet. Contact your Clay account team.
