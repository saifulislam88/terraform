### What are the issues with using S3-only for state locking in Terraform❓ 

✅ When using S3-only (without DynamoDB) for storing Terraform state files:
- S3 does **not support automatic locking**.
- If a Terraform execution (e.g., via CI/CD or GitHub runner) **crashes**, the lock file remains in S3.
- You must **manually find and delete** the lock file, which is time-consuming and error-prone.
- It's particularly problematic when using **spot instances** or **self-hosted GitHub runners** that may terminate unexpectedly.
