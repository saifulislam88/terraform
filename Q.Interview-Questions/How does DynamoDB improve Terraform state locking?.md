### How does DynamoDB improve Terraform state locking❓

✅ DynamoDB provides a native and efficient way to manage state locks by:
- Automatically handling lock acquisition and release.
- Allowing quick and easy cleanup of stale locks using the AWS console or CLI.
- Preventing concurrent operations safely in CI/CD pipelines.
- Supporting filter operations on `LockID` to find stale locks quickly.
