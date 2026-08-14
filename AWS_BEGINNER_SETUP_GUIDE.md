# AWS Setup Guide: S3 + SQS + Lambda

## Status and scope

The learning resources in this guide have been created in the recorded account.
The successful-message path is configured; the invalid-message retry exercise
has passed its retry-to-DLQ confirmation. These resources prove the basic
`SQS -> Lambda -> S3` path and are not production pipeline resources.

This guide creates a small private learning system:

```text
SQS message → Lambda → S3 JSON file
```

Do not create the production pipeline yet. Finish this sandbox first.

## Names used in this guide

Recorded learning values:

```text
Project: storesignal
Environment: dev
AWS profile: storesignal-dev
Project Region: ap-south-2
IAM Identity Center Region: eu-north-1
S3 bucket: signalshop-buk
SQS dead-letter queue: storesignal-dev-learning-dlq
SQS source queue: storesignal-dev-learning
Lambda function: storesignal-dev-learning-worker
```

S3, SQS, and Lambda use Hyderabad, `ap-south-2`. IAM Identity Center is
configured in `eu-north-1`; that control-plane Region does not change the
project-resource Region.

---

## Part 1 — Create the AWS account

1. Open [Create an AWS account](https://docs.aws.amazon.com/accounts/latest/reference/getting-started.html).
2. Choose **Create an AWS Account**.
3. Enter an email address that you control permanently.
4. Choose a strong, unique root password.
5. Enter your contact and payment information.
6. Complete phone and email verification.
7. Choose the **Paid account plan** if this account will eventually run the deployed application.
8. Wait for the account-activation email.
9. Sign in as **Root user** once to secure the account.

> The current AWS Free plan is time- and credit-limited. Enabling AWS Organizations for IAM Identity Center can upgrade a Free-plan account and end its credits. Read [AWS account plan differences](https://docs.aws.amazon.com/awsaccountbilling/latest/aboutv2/free-tier-plans.html) before choosing.

## Part 2 — Protect the root account

1. In the AWS console, choose your account name in the top-right corner.
2. Choose **Security credentials**.
3. Find **Multi-factor authentication (MFA)**.
4. Choose **Assign MFA device**.
5. Prefer a passkey or hardware security key. A trusted authenticator application is also acceptable.
6. Complete the MFA setup.
7. Store recovery information safely.
8. Confirm the account email and telephone number are correct.
9. Do **not** create an access key for the root user.
10. Stop using the root user for ordinary work after Part 4.

AWS requires root MFA and recommends phishing-resistant MFA where possible: [Root MFA guide](https://docs.aws.amazon.com/IAM/latest/UserGuide/enable-mfa-for-root.html).

## Part 3 — Create cost alerts before resources

1. Search for **Billing and Cost Management** in the AWS console.
2. Open **Budgets**.
3. Choose **Create budget**.
4. Choose **Customize (advanced)**.
5. Choose **Cost budget**.
6. Set:

   ```text
   Name: storesignal-monthly-budget
   Period: Monthly
   Budget renewal type: Recurring budget
   Budget amount: USD 20
   ```

7. Add alerts to your email at:

   ```text
   50% actual spend
   80% actual spend
   100% forecasted spend
   ```

8. Review and create the budget.
9. Enable Free Tier usage alerts if AWS presents that option in Billing Preferences.
10. Remember: a budget sends alerts; it does not automatically stop every AWS service.

Official instructions: [Creating an AWS Budget](https://docs.aws.amazon.com/cost-management/latest/userguide/budgets-create.html).

## Part 4 — Create your everyday AWS login

Use IAM Identity Center so your CLI receives temporary credentials rather than permanent access keys.

1. While signed in as root, search for **IAM Identity Center**.
2. Open it in your chosen Region.
3. Choose **Enable**.
4. Choose the organization-based setup when prompted.
5. Open **Users**.
6. Choose **Add user**.
7. Enter your name and an email address you can access.
8. Send the invitation email.
9. Open **AWS accounts**.
10. Select your AWS account.
11. Choose **Assign users or groups**.
12. Select the user you just created.
13. Create or select the predefined **AdministratorAccess** permission set for initial setup.
14. Complete the assignment.
15. Open the invitation email.
16. Set the user password and MFA.
17. Sign out of the root account.
18. Sign in through the AWS access portal as the new user.
19. Use this user for all remaining steps.

Official walkthrough: [IAM Identity Center quick start](https://docs.aws.amazon.com/singlesignon/latest/userguide/awsapps-identity-center-quick-start.html).

## Part 5 — Pick and remember one Region

1. Look at the Region selector in the top-right of the AWS console.
2. Select your chosen Region.
3. Write down both its display name and code.
Recorded selection:

```text
Display name: Asia Pacific (Hyderabad)
Code: ap-south-2
```

4. Check the Region selector every time you open a service. Resources in different Regions will not appear together.

## Part 6 — Install and configure the AWS CLI

### 6.1 Check whether it is already installed

Run:

```bash
aws --version
```

You want AWS CLI version 2. If it is missing, follow the official [AWS CLI v2 Linux installation guide](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html).

### 6.2 Configure temporary SSO access

1. In the AWS console, open **IAM Identity Center**.
2. Open **Settings**.
3. Copy the **AWS access portal URL**.
4. In the terminal, run:

   ```bash
   aws configure sso
   ```

5. Answer the prompts:

   ```text
   SSO session name: storesignal
   SSO start URL: paste the AWS access portal URL
   SSO Region: the Region shown by IAM Identity Center
   SSO registration scopes: press Enter for the default
   AWS account: choose your account
   Role: choose AdministratorAccess
   Default client Region: your chosen project Region
   Default output format: json
   Profile name: storesignal-dev
   ```

6. A browser opens. Approve the sign-in.
7. Verify the profile:

   ```bash
   aws sso login --profile storesignal-dev
   aws sts get-caller-identity --profile storesignal-dev
   ```

8. The second command should display your account and assumed-role identity.
9. Never copy temporary credentials into this repository or `.env` files.

Official instructions: [Configure AWS CLI with IAM Identity Center](https://docs.aws.amazon.com/cli/latest/userguide/cli-configure-sso.html).

## Part 7 — Create the private S3 bucket

1. Search for **S3** in the AWS console.
2. Open **General purpose buckets**.
3. Choose **Create bucket**.
4. Select your chosen Region.
5. Enter the recorded globally unique name:

   ```text
   signalshop-buk
   ```

6. Leave **Object Ownership** as **Bucket owner enforced**.
7. Leave all **Block Public Access** boxes enabled.
8. Do not add a public bucket policy.
9. Enable **Bucket Versioning** for the learning exercise.
10. Under default encryption, choose **Server-side encryption with Amazon S3 managed keys (SSE-S3)**.
11. Do not choose a KMS key.
12. Add tags:

    ```text
    Project = storesignal
    Environment = dev
    ManagedBy = manual-learning
    ```

13. Choose **Create bucket**.

AWS recommends keeping Block Public Access enabled. Bucket names are globally unique and the Region cannot be changed later: [Create an S3 bucket](https://docs.aws.amazon.com/AmazonS3/latest/userguide/create-bucket-overview.html).

### 7.1 Current lifecycle rule for sandbox files

The configured rule is named:

   ```text
   delete-learning-artifacts
   ```

It is limited to this prefix:

   ```text
   learning/
   ```

Its only configured action is **abort incomplete multipart uploads after 7
days**. It does not expire completed current objects, noncurrent versions, or
delete markers. Completed learning artifacts therefore remain until they are
manually removed or an explicit expiration action is approved and added.

Do not infer a production `runs/` retention policy from this learning rule.
Production retention must be selected explicitly in the implementation plan.

## Part 8 — Create the SQS dead-letter queue

Create the dead-letter queue first because the main queue must reference it.

1. Search for **SQS**.
2. Choose **Create queue**.
3. Select **Standard**.
4. Enter:

   ```text
   storesignal-dev-learning-dlq
   ```

5. Set message retention to 14 days.
6. Enable server-side encryption.
7. Choose the **Amazon SQS key (SSE-SQS)**, not KMS.
8. Leave access policy as the basic owner-only policy.
9. Add the same `Project`, `Environment`, and `ManagedBy` tags.
10. Choose **Create queue**.

SQS does not create a DLQ automatically: [Configure an SQS dead-letter queue](https://docs.aws.amazon.com/AWSSimpleQueueService/latest/SQSDeveloperGuide/sqs-configure-dead-letter-queue.html).

## Part 9 — Create the SQS source queue

1. Choose **Create queue** again.
2. Select **Standard**.
3. Enter:

   ```text
   storesignal-dev-learning
   ```

4. Set:

   ```text
   Visibility timeout: 6 minutes
   Message retention: 4 days
   Delivery delay: 0 seconds
   Receive message wait time: 0 seconds
   Maximum message size: leave the default
   ```

5. Enable server-side encryption.
6. Choose **Amazon SQS key (SSE-SQS)**.
7. Enable **Dead-letter queue**.
8. Select `storesignal-dev-learning-dlq`.
9. Set **Maximum receives** to `5`.
10. Add the project tags.
11. Choose **Create queue**.

## Part 10 — Create the Lambda function

1. Search for **Lambda**.
2. Open **Functions**.
3. Choose **Create function**.
4. Choose **Author from scratch**.
5. Enter:

   ```text
   Function name: storesignal-dev-learning-worker
   Runtime: Node.js 24.x
   Architecture: x86_64
   Permissions: Create a new role with basic Lambda permissions
   ```

6. Choose **Create function**.
7. Open **Configuration → General configuration → Edit**.
8. Set:

   ```text
   Memory: 256 MB
   Timeout: 1 minute
   ```

9. Save.

The automatically created role initially permits logging only. Every Lambda needs an execution role: [Lambda execution-role permissions](https://docs.aws.amazon.com/lambda/latest/dg/lambda-permissions.html).

## Part 11 — Give Lambda permission to write only to the learning folder

1. In the Lambda function, open **Configuration → Permissions**.
2. Choose the execution-role name. This opens IAM.
3. Choose **Add permissions → Create inline policy**.
4. Choose the **JSON** editor.
5. Paste the policy below.
6. Replace `YOUR_BUCKET_NAME` with the exact bucket name.

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "WriteLearningArtifacts",
      "Effect": "Allow",
      "Action": [
        "s3:PutObject"
      ],
      "Resource": "arn:aws:s3:::YOUR_BUCKET_NAME/learning/*"
    }
  ]
}
```

7. Choose **Next**.
8. Name it:

   ```text
   StoreSignalLearningS3Write
   ```

9. Create the policy.

## Part 12 — Add the bucket name to Lambda

1. Return to the Lambda function.
2. Open **Configuration → Environment variables**.
3. Choose **Edit**.
4. Add:

   ```text
   Key: ARTIFACT_BUCKET
   Value: your exact S3 bucket name
   ```

5. Save.

Do not put secrets in this learning function.

## Part 13 — Add the learning Lambda code

1. Open the **Code** tab.
2. Replace the generated contents of `index.mjs` with:

```javascript
import { PutObjectCommand, S3Client } from "@aws-sdk/client-s3";

const s3 = new S3Client({});

export const handler = async (event) => {
  const failures = [];

  for (const record of event.Records ?? []) {
    try {
      const payload = JSON.parse(record.body);
      const output = {
        messageId: record.messageId,
        receivedAt: new Date().toISOString(),
        payload
      };

      await s3.send(new PutObjectCommand({
        Bucket: process.env.ARTIFACT_BUCKET,
        Key: `learning/${record.messageId}.json`,
        Body: JSON.stringify(output, null, 2),
        ContentType: "application/json"
      }));
    } catch (error) {
      console.error("record_failed", {
        messageId: record.messageId,
        error: error instanceof Error ? error.message : String(error)
      });
      failures.push({ itemIdentifier: record.messageId });
    }
  }

  return { batchItemFailures: failures };
};
```

3. Choose **Deploy**.

## Part 14 — Connect SQS to Lambda

1. In the Lambda function overview, choose **Add trigger**.
2. Select **SQS**.
3. Choose `storesignal-dev-learning`.
4. Set batch size to `1`.
5. Enable the trigger.
6. Open additional settings if available.
7. Enable **Report batch item failures**.
8. Set maximum concurrency to `2` if the console offers the setting.
9. Choose **Add**.

If AWS reports missing SQS permissions:

1. Open the Lambda execution role again.
2. Choose **Add permissions → Attach policies**.
3. Attach `AWSLambdaSQSQueueExecutionRole`.
4. Return to Lambda and add the trigger again.

The queue and Lambda must be in the same Region. AWS recommends a queue visibility timeout at least six times the Lambda timeout and a `maxReceiveCount` of at least five: [Configure SQS as a Lambda event source](https://docs.aws.amazon.com/lambda/latest/dg/services-sqs-configure.html).

## Part 15 — Send the first message

1. Open SQS.
2. Open `storesignal-dev-learning`.
3. Choose **Send and receive messages**.
4. Paste this message body:

```json
{
  "runId": "run_learning_001",
  "queryId": "query_learning_001",
  "message": "hello from SQS"
}
```

5. Choose **Send message**.
6. Wait approximately 10–30 seconds.
7. Open the S3 bucket.
8. Open the `learning/` prefix.
9. Open the new JSON object.
10. Confirm it contains the message you sent.

The successful sequence is now:

```text
You → SQS → Lambda → S3
```

## Part 16 — Perform one retry test

1. Temporarily change the SQS message to invalid JSON:

   ```text
   this is not json
   ```

2. Send it.
3. Open the Lambda function.
4. Open **Monitor → View CloudWatch logs**.
5. Confirm that `record_failed` appears.
6. Wait for SQS retries.
7. After five receives, confirm the message appears in `storesignal-dev-learning-dlq`.
8. Do not purge the queue until you have inspected the failed message.

Lambda processes SQS messages at least once, so duplicate delivery is possible and workers must be idempotent: [Using Lambda with SQS](https://docs.aws.amazon.com/lambda/latest/dg/with-sqs.html).

## Part 17 — Verify everything from the CLI

Use the recorded names and Region:

```bash
aws s3api head-bucket \
  --bucket signalshop-buk \
  --profile storesignal-dev

aws sqs get-queue-url \
  --queue-name storesignal-dev-learning \
  --region ap-south-2 \
  --profile storesignal-dev

aws lambda get-function \
  --function-name storesignal-dev-learning-worker \
  --region ap-south-2 \
  --profile storesignal-dev
```

All three commands should succeed without displaying secret credentials.

## Part 18 — Stop here and record these values

Record only these non-secret values:

```text
AWS account ID: 074209491031
AWS profile name: storesignal-dev
AWS project Region: ap-south-2
IAM Identity Center Region: eu-north-1
S3 bucket name: signalshop-buk
SQS source queue name: storesignal-dev-learning
SQS dead-letter queue name: storesignal-dev-learning-dlq
Lambda function name: storesignal-dev-learning-worker
Learning test result: passed — the same invalid message failed five receives and is present in the DLQ
```

Do not send or commit:

```text
Passwords
MFA codes or recovery codes
Access-key IDs
Secret-access keys
SSO tokens
Session tokens
Neon credentials
Provider API keys
```

The learning test has passed. Execute the required probes at the end of
`PRELIMINARY_LAMBDA_SQS_S3_MIGRATION_PLAN.md`. Production queues, Lambda
functions, IAM policies, payload contracts, concurrency settings, and database
changes are created only after the final parent-agent implementation checklist
is reviewed.

## If you need to stop and avoid ongoing sandbox use

Disable the Lambda SQS trigger:

1. Open the Lambda function.
2. Open **Configuration → Triggers**.
3. Select the SQS trigger.
4. Choose **Edit**.
5. Disable the trigger.

The budget remains active. The current S3 lifecycle rule only aborts incomplete
multipart uploads after 7 days; it does not delete completed objects under
`learning/`. Do not delete the resources until payload discovery is complete
unless you intentionally want to recreate the exercise.
