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
   -  User B tries `terraform apply` → ❌ gets error: `Error acquiring the state lock`

✅ **Key Point**:\
Always enable **remote state locking** (e.g., with DynamoDB for S3 backend) when working in teams to **ensure consistency and safety**.
