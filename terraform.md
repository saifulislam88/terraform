https://www.linkedin.com/pulse/day-60-terraform-sayali-shewale/ \
https://www.linkedin.com/pulse/terraform-muhammad-junaid-usman-9vfhf/ \
https://www.linkedin.com/pulse/terraform-guide-yash-kumar-zoryc/



### What is Terraform?
Terraform is an infrastructure as code (IaC) tool that allows you to create, manage, and update infrastructure resources such as virtual machines, networks, and storage in a repeatable, scalable, and automated way.


### Install Terraform

- **Step 1: Adding repo and Package Installation**
First, you'll need to install Terraform on your local machine(**For Ubuntu**)

```bash
sudo apt-get update && sudo apt-get install -y gnupg software-properties-common curl
curl -fsSL https://apt.releases.hashicorp.com/gpg | sudo apt-key add -
sudo apt-add-repository "deb [arch=amd64] https://apt.releases.hashicorp.com $(lsb_release -cs) main"
sudo apt-get update -y && sudo apt-get install terraform -y 
```

- **Step 2: AWS CLI Setup and Authentication**
  
**Install the AWS CLI if you haven’t already:**
```sh
sudo apt-get update
sudo apt-get install awscli -y
```




# How to Obtain AWS Credentials and Set Default Region

## 1. AWS Access Key ID & Secret Access Key

### For a New User:
1. Log in to the AWS Management Console.
2. Navigate to the **IAM (Identity and Access Management)** service.
3. Under **Access management**, click on **Users**.
4. Select the user you want to configure, or create a new user if needed.
5. In the user details, go to the **Security credentials** tab.
6. Scroll down to the **Access keys** section.
7. Click on **Create access key**.
8. Once created, you will see the **Access Key ID** and **Secret Access Key**. 
   - **Important:** Copy them immediately as you will not be able to see the secret key again.

### For an Existing User:
- If you already have an Access Key and Secret Access Key, you can find it under the same **Security credentials** tab for the user in the IAM console.

## 2. Default Region Name
The region name corresponds to the AWS region you want to set as default for your CLI commands. Some common region names are:

- `us-east-1` (N. Virginia)
- `us-west-2` (Oregon)
- `eu-west-1` (Ireland)
- `ap-south-1` (Mumbai)
- `ap-southeast-1` (Singapore)

Choose the region closest to you or the one where your resources will be deployed.




**Configure your AWS credentials:**
Once you have your Access Key ID, Secret Access Key, and Default Region Name, you can configure the AWS CLI using the following command:

`aws configure`

**You'll be prompted to enter the values:**
![image](https://github.com/user-attachments/assets/4151cb7e-de28-4fdb-a559-40bc75ea5217)

Provide your AWS Access Key ID, Secret Access Key, region, and output format.
`
