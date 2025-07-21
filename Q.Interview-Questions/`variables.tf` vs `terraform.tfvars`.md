
### 🎯 Terraform: `variables.tf` vs `terraform.tfvars` Explained with Real Example

Understanding the difference is **key for interviews and real-world usage**. Here's a simple explanation:

---

#### 📘 `variables.tf` — Define Variables

This file is used to **declare** the variables Terraform expects.

##### ✅ Example:
```hcl
# variables.tf
variable "region" {
  description = "AWS region"
  type        = string
  default     = "us-east-1"
}

variable "vpc_cidr" {
  description = "CIDR block for the VPC"
  type        = string
}
```

---

#### 📒 `terraform.tfvars` — Assign Values

This file is used to **provide actual values** for the variables declared above.

##### ✅ Example:
```hcl
# terraform.tfvars
vpc_cidr = "10.0.0.0/16"
```

Terraform automatically loads this file when running `terraform plan` or `terraform apply`.

---

#### 🔄 What Happens with Defaults?

If a variable has a **default value**, you don’t need to define it in `terraform.tfvars`.

##### Example:
- `region` has a default of `"us-east-1"` → no need to set it in `terraform.tfvars`
- `vpc_cidr` has no default → MUST be provided or Terraform will throw an error

---

#### ⚠️ Real-World Interview Scenario

##### ❓ Question:
> What will happen if you forget to provide a required variable that has no default?

##### ✅ Answer:
Terraform will throw a **"missing required variable"** error.

##### 💥 Example Error:
```
Error: Missing required variable

The argument "vpc_cidr" is required, but no definition was found.
```

##### ✅ Fix:
Add it in `terraform.tfvars`, use `-var="vpc_cidr=value"` in CLI, or add a default in `variables.tf`.

---

#### 🧪 Bonus Tip: Use CLI or Custom Files

You can override values with:

```bash
terraform apply -var="vpc_cidr=10.2.0.0/16"
terraform apply -var-file="prod.tfvars"
```

---

#### ✅ Summary Table

| File               | Purpose                         | Required?                 |
|--------------------|----------------------------------|---------------------------|
| `variables.tf`     | Declares variable types & defaults | ✅ Yes                     |
| `terraform.tfvars` | Supplies variable values         | ❌ Optional (if defaults exist) |

---

🛠 Use `variables.tf` to define *what* inputs are needed, and `terraform.tfvars` to define *the actual values* used per environment or team member.
