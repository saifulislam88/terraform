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

### Core Concepts and Terminology

- **What is Infrastructure as Code (IaC)?**
Infrastructure as Code (IaC) is a practice of managing and provisioning infrastructure using code instead of manual processes. By treating infrastructure as code, teams can version control their infrastructure, automate the provisioning process, and improve collaboration between different teams. IaC enables teams to make changes to infrastructure in a safe and repeatable way, and it helps to reduce the risk of human error and inconsistencies.

- **What is Resource?**
In Terraform, a resource is a declarative representation of a component in a cloud infrastructure, such as a virtual machine, database, or network interface. Resources define the desired state of the component, and Terraform uses the resource definition to create, modify, or delete the component as needed.

- **What is Provider?**
In Terraform, a provider is a plugin that interfaces with a specific cloud infrastructure provider or service. Providers define the resources that Terraform can manage, as well as the methods for creating, updating, and deleting those resources. Examples of providers include AWS, Google Cloud, and Microsoft Azure.

- **What is State file in terraform? What’s the importance of it ?**
The Terraform state file is a JSON file that stores the state of the infrastructure managed by Terraform. It includes information about the resources that have been created, their current state, and any dependencies between them. The state file is critical to Terraform's operation, as it is used to plan and execute changes to the infrastructure. The state file should be kept in a safe and secure location, as it contains sensitive information about the infrastructure.

- **What is Desired and Current State?**
In Terraform, the desired state is the state that you want your infrastructure to be in, as defined in your Terraform configuration files. The current state is the actual state of the infrastructure, as represented in the Terraform state file. When you run terraform apply, Terraform compares the desired state with the current state and makes changes as needed to bring the infrastructure into the desired state.






Understanding Terraform Basics

Terraform Commands


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

- **Step 2: Configure your AWS credentials**\

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






