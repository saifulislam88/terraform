### What is Terraform state locking and why is it important❓
 
✅ **Terraform State Locking**:\
**State locking** prevents **multiple users** from **modifying the same Terraform state at the same tim**e, avoiding corruption or race conditions.

⚠️ **Why it's important**:\
Without locking, two people running `terraform apply` simultaneously could:
- Overwrite each other's changes
- Cause **inconsistent infrastructure**
- Corrupt the `terraform.tfstate` file

🔐 **Real Example**:
Using S3 + DynamoDB backend:
   -  User A runs `terraform apply`
   -  Terraform locks the state in DynamoDB
   -  User B tries `terraform apply` → ❌ gets error: `Error acquiring the state lock` | `Error: Error locking state`

✅ **Key Point**:\
Always enable **remote state locking** (e.g., with `DynamoDB` for `S3 backend`) when working in teams to **ensure consistency and safety**.





#### Terraform Remote State with S3 + DynamoDB Locking

##### ✅ 1. Create S3 Bucket for Terraform State

This will store your `terraform.tfstate` file.

```bash
aws s3api create-bucket \
  --bucket my-terraform-state-bucket \
  --region us-east-1
```

➡️ *(Replace `my-terraform-state-bucket` & region as needed)*

---

##### ✅ 2. Create DynamoDB Table for Locking

This will handle state file locks.

```bash
aws dynamodb create-table \
  --table-name terraform-locks \
  --attribute-definitions AttributeName=LockID,AttributeType=S \
  --key-schema AttributeName=LockID,KeyType=HASH \
  --billing-mode PAY_PER_REQUEST
```

---

##### ✅ 3. Add Remote Backend to Terraform Code

In a file like `backend.tf` (or directly in `main.tf`), add:

```hcl
terraform {
  backend "s3" {
    bucket         = "my-terraform-state-bucket"
    key            = "project-name/env-name/terraform.tfstate"
    region         = "us-east-1"
    dynamodb_table = "terraform-locks"
    encrypt        = true
  }
}
```

> 💡 The `key` is the path to the `.tfstate` file inside the bucket.

---

##### ✅ 4. Initialize Backend

Run this once (or when the backend config changes):

```bash
terraform init
```

Expected output:
```
Terraform has been successfully initialized!
```

---

##### ✅ 5. Test Locking

Try running `terraform apply` from **two terminals at the same time**.  
The second one should show:

```
Error: Error locking state
```

✅ This confirms that **state locking is working** properly and prevents simultaneous changes.
