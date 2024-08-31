https://www.linkedin.com/pulse/day-60-terraform-sayali-shewale/ \
https://www.linkedin.com/pulse/terraform-muhammad-junaid-usman-9vfhf/ \
https://www.linkedin.com/pulse/terraform-guide-yash-kumar-zoryc/



### What is Terraform?
Terraform is an infrastructure as code (IaC) tool that allows you to create, manage, and update infrastructure resources such as virtual machines, networks, and storage in a repeatable, scalable, and automated way.


### Why Use Terraform?

**Consistency:** Define infrastructure in code, ensuring a consistent deployment process. \
**Automation:** Automate the provisioning and management of infrastructure, reducing the potential for manual errors. \
**Version Control:** Infrastructure configurations can be versioned, rolled back, and reviewed just like application code. \
**Provider-Agnostic:** Terraform supports multiple cloud providers, enabling multi-cloud deployments.

### Basic Terraform Workflow

Terraform’s workflow consists of three main steps:

**Write:** Define the infrastructure in high-level configuration files.\
**Plan:** Preview the changes Terraform will make to reach the desired state.\
**Apply:** Apply the changes to achieve the desired state.



### Core Concepts and Terminology

- **What is Infrastructure as Code (IaC)?**
Infrastructure as Code (IaC) is a practice of managing and provisioning infrastructure using code instead of manual processes. By treating infrastructure as code, teams can version control their infrastructure, automate the provisioning process, and improve collaboration between different teams. IaC enables teams to make changes to infrastructure in a safe and repeatable way, and it helps to reduce the risk of human error and inconsistencies.

- **What is Resource?**
In Terraform, a resource is a declarative representation of a component in a cloud infrastructure, such as a `virtual machine`, `database`, or `network interface` ,`VPC`,`Kubernetes`. Resources define the desired state of the component, and Terraform uses the resource definition to `create`, `modify`, or `delete` the component as needed.

- **What is Provider?**
In Terraform, a provider is a plugin that interfaces with a specific cloud infrastructure provider or service. Providers define the resources that Terraform can manage, as well as the methods for creating, updating, and deleting those resources. Examples of providers include `AWS`, `Google Cloud`, and `Microsoft Azure`.

- **What is State file in terraform? What’s the importance of it ?**
The Terraform state file is a `JSON` file that stores the state of the infrastructure managed by Terraform. It includes information about the resources that have been created, their current state, and any dependencies between them. The state file is critical to Terraform's operation, as it is used to plan and execute changes to the infrastructure. The state file should be kept in a safe and secure location, as it contains sensitive information about the infrastructure.

- **What is Desired and Current State?**
In Terraform, the desired state is the state that you want your infrastructure to be in, as defined in your Terraform configuration files. The current state is the actual state of the infrastructure, as represented in the Terraform state file. When you run terraform apply, Terraform compares the desired state with the current state and makes changes as needed to bring the infrastructure into the desired state.



Understanding Terraform Basics


### Install Terraform

- **Step 1: Adding repo and Package Installation**
First, you'll need to install Terraform on your local machine(**For Ubuntu**)

```bash
sudo apt-get update && sudo apt-get install -y gnupg software-properties-common curl
curl -fsSL https://apt.releases.hashicorp.com/gpg | sudo apt-key add -
sudo apt-add-repository "deb [arch=amd64] https://apt.releases.hashicorp.com $(lsb_release -cs) main"
sudo apt-get update -y && sudo apt-get install terraform -y 
```

- **Step 2: AWS CLI Setup and Authentication - Install the AWS CLI if you haven’t already:**

```sh
sudo apt-get update
sudo apt-get install awscli -y
```
`terraform -version`

- **Step 2: Configure your AWS credentials**

Once you have your Access Key ID, Secret Access Key, and Default Region Name, you can configure the AWS CLI using the following command:

```sh
aws configure
```

**You'll be prompted to enter the values:**
![image](https://github.com/user-attachments/assets/4151cb7e-de28-4fdb-a559-40bc75ea5217)

Provide your AWS Access Key ID, Secret Access Key, region, and output format.


### How to Obtain AWS Credentials and Set Default Region

#### 1. AWS Access Key ID & Secret Access Key

#### For a New User:
1. Log in to the AWS Management Console.
2. Navigate to the **IAM (Identity and Access Management)** service.
3. Under **Access management**, click on **Users**.
4. Select the user you want to configure, or create a new user if needed.
5. In the user details, go to the **Security credentials** tab.
6. Scroll down to the **Access keys** section.
7. Click on **Create access key**.
8. Once created, you will see the **Access Key ID** and **Secret Access Key**. 
   - **Important:** Copy them immediately as you will not be able to see the secret key again.

#### For an Existing User:
- If you already have an Access Key and Secret Access Key, you can find it under the same **Security credentials** tab for the user in the IAM console.

#### 2. Default Region Name
The region name corresponds to the AWS region you want to set as default for your CLI commands. Some common region names are:

- `us-east-1` (N. Virginia)
- `us-west-2` (Oregon)
- `eu-west-1` (Ireland)
- `ap-south-1` (Mumbai)
- `ap-southeast-1` (Singapore)

Choose the region closest to you or the one where your resources will be deployed.


### Terraform Project Structure

When working with Terraform, it's best practice to organize your configuration into separate files for better maintainability and clarity. Here’s how we can structure the Terraform project:

```plaintext
eks-cluster/
├── main.tf          
├── variables.tf    
├── outputs.tf       
├── provider.tf 
├── terraform.tfstate
```

### File Breakdown

#### `provider.tf`
- **Purpose**: This file contains the provider configurations, such as AWS, Azure, or GCP. Providers are responsible for managing the infrastructure resources.
- **Example**:
    ```hcl
    provider "aws" {
      region = var.region
    }
    ```

#### `variables.tf`
- **Purpose**: This file is used to define input variables, which are used throughout the Terraform configuration. It helps in parameterizing the values, making the code reusable and adaptable to different environments.
- **Example**:
    ```hcl
variable "region" {
  description = "The AWS region to deploy resources in."
  type        = string
  default     = "us-west-2"
}

variable "ami" {
  description = "The AMI ID for the instance."
  type        = string
  default     = "ami-0c55b159cbfafe1f0"
}

variable "instance_type" {
  description = "The type of instance to use."
  type        = string
  default     = "t2.micro"
}


    ```

#### `main.tf`
- **Purpose**: This is the core file where you define the actual resources, modules, and other components of your infrastructure. This is the heart of your Terraform configuration.
- **Example**:
    ```hcl
resource "aws_instance" "example" {
  ami           = var.ami
  instance_type = var.instance_type
}
    ```

#### `outputs.tf`
- **Purpose**: This file defines the output values that you want Terraform to display after the execution. Outputs can be used to extract information from your resources, such as instance IDs or public IPs, which can be useful for referencing later.
- **Example**:
    ```hcl
    output "instance_id" {
      value = aws_instance.example.id
    }
    ```

#### `terraform.tfstate`
- **Purpose**: This file is automatically generated by Terraform and stores the state of your infrastructure. It’s crucial for keeping track of your deployed resources and making updates.
- **Note**: You don't need to manually create or edit this file; Terraform handles it for you.

### Sequence of Usage

1. **Start with `provider.tf`**: Define the providers you will use, like AWS or Azure.
2. **Set up `variables.tf`**: Define any input variables needed by your configuration.
3. **Build `main.tf`**: This is where you define your actual resources, such as VPCs, instances, and other infrastructure components.
4. **Use `outputs.tf`**: Add any outputs that you want to extract and display after running Terraform.
5. **Run Terraform**: After writing your configurations, you run commands like `terraform init`, `terraform plan`, and `terraform apply`, which will generate the `terraform.tfstate` file.


### Terraform Commands

**terraform init**: Initializes a Terraform configuration.\
**terraform plan**: Creates an execution plan.\
**terraform apply**: Executes the plan.\
**terraform destroy**: Destroys the infrastructure managed by Terraform.\
**terraform fmt**: Formats the Terraform files.\
**terraform validate**: Validates the configuration.







