
### How do you clean up stale locks in S3 vs DynamoDB?

| Operation       | DynamoDB                        | S3-only                          |
|----------------|----------------------------------|----------------------------------|
| View locks      | Filter by non-empty LockID      | Browse each folder manually      |
| Delete locks    | Select & delete (3 clicks)      | Manually confirm deletion every time |
| Automation Ready| ✅ Yes                           | ❌ No                            |
