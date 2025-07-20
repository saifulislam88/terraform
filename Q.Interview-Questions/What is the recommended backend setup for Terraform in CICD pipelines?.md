### What is the recommended backend setup for Terraform in CI/CD pipelines?

✅ Use **S3 for state storage** and **DynamoDB for state locking**. This combo provides reliable and scalable state management, especially in:
- CI/CD pipelines (e.g., GitHub Actions, GitLab CI)
- Multi-account AWS setups
- Large-scale infrastructure automation
