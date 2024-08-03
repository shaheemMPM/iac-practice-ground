
# EC2 Instance Terraform Configuration with Ansible Integration

This project uses Terraform to create an EC2 instance in AWS and Ansible to deploy a Node.js application on it.

## What it does

1. Creates a new RSA key pair
2. Saves the private key to a local file
3. Sets up a security group allowing inbound traffic on port 3000
4. Creates an EC2 instance with specified AMI and instance type
5. Tags the instance with a provided name
6. Generates a dynamic Ansible inventory
7. Runs an Ansible playbook to set up and deploy a Node.js application

## Prerequisites

- Terraform installed on your local machine
- Ansible installed on your local machine
- AWS account with appropriate permissions
- AWS CLI configured with your credentials (optional)

## Usage

1. Clone this repository.

2. Initialize Terraform:
    ```bash
    terraform init
    ```

3. Plan the Terraform execution:
    ```bash
    terraform plan
    ```

4. Apply the Terraform configuration:
    ```bash
    terraform apply
    ```
    You will be prompted to enter values for the variables if not provided.

5. The Ansible playbook will run automatically after the EC2 instance is created.

6. To destroy the created resources when you're done:
    ```bash
    terraform destroy
    ```

## One-step Execution

You can also run the entire process in one step by providing all variable values in the command line:

```bash
terraform apply -auto-approve \
-var="access_key=<YOUR_AWS_ACCESS_KEY>" \
-var="secret_key=<YOUR_AWS_SECRET_KEY>" \
-var="region=<AWS_REGION>" \
-var="key_name=<PEM_FILE.pem>" \
-var="instance_type=<AWS_INSTANCE_TYPE>" \
-var="ami_id=<AWS_AMI_ID_FOR_SELECTED_ZONE>" \
-var="instance_name=<EC2_INSTANCE_NAME>"
```
Replace the placeholders (enclosed in <>) with your actual values.

## Ansible Configuration
The Ansible playbook (`node-express.yml`) performs the following tasks:

1. Installs Node.js and npm
2. Clones a specified Git repository containing a Node.js application
3. Installs application dependencies
4. Sets up and starts the application using PM2

You can modify the Ansible playbook to suit your specific deployment needs.

### Note
- The private key for SSH access will be saved in the current directory with the name specified in `key_name`. Ensure to keep this file secure and do not commit it to version control.
- The Node.js application will be accessible at `http://<EC2_PUBLIC_IP>:3000` after deployment.
- Ensure your AWS credentials have the necessary permissions to create EC2 instances and security groups.
