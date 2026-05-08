# AWS File Upload Scanner

An automated serverless file scanning pipeline built on AWS. When a file is uploaded to S3, a Lambda function instantly checks it for dangerous file types and size limits. Approved files are moved to a processed bucket. Blocked files are automatically deleted.

---

## AWS Services Used

- **S3** — two buckets for incoming uploads and processed files
- **Lambda** — serverless function that scans and routes every file
- **CloudWatch** — automatic logging of every file processed
- **IAM** — least privilege role scoped to only what Lambda needs

---

## How It Works

1. User uploads a file to the incoming S3 bucket
2. S3 automatically triggers the Lambda function
3. Lambda checks the file extension and file size
4. If the file is dangerous or too large it gets deleted immediately
5. If the file is safe it gets moved to the processed bucket with a timestamp prefix

---

## What Gets Blocked

- Dangerous extensions: `.exe` `.bat` `.sh` `.php` `.py` `.rb` `.ps1` `.cmd` `.vbs` `.js`
- Any file over 10MB

---

## Setup

1. Create two S3 buckets in the same region — one incoming, one processed
2. Create an IAM role with S3 and CloudWatch permissions
3. Deploy the Lambda function using Node.js 20.x
4. Add an S3 trigger on the incoming bucket for all object create events
5. Upload a test file and watch it move to the processed bucket automatically

---

## What I Learned

- How S3 event triggers invoke Lambda functions automatically
- Serverless file processing patterns used in real production systems
- IAM least privilege principles for securing AWS services
- CloudWatch logging for observability and debugging
- Routing files between S3 buckets programmatically

---

## Free Tier

This project runs entirely within the AWS free tier.
- Lambda: 1 million free requests per month
- S3: 5GB free storage
- CloudWatch: 5GB free log ingestion per month
