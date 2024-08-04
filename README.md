# Multi-Cloud Infrastructure as Code with Terraform and Ansible

This project uses Terraform to create cloud instances and Ansible to deploy applications across multiple cloud providers and frameworks.

## What it does

1. Provides a modular structure for different cloud providers and frameworks
2. Creates necessary cloud resources (e.g., EC2 instances for AWS)
3. Sets up security groups and networking
4. Generates SSH key pairs for secure access
5. Uses Ansible to deploy and configure applications

## Prerequisites

- Terraform installed on your local machine
- Ansible installed on your local machine
- Accounts and necessary permissions for supported cloud providers (AWS, Azure, GCP)
- Respective CLI tools configured with your credentials (optional)

## Project Structure
```
.
└── terraform
├── aws
│   ├── laravel
│   └── node
│       ├── ansible.cfg
│       ├── inventory.tpl
│       ├── main.tf
│       ├── playbook.yml
│       └── variables.tf
├── azure
└── gcp
```

## Usage

1. Clone this repository.

2. Navigate to the desired provider and framework directory:
    ```bash
    cd terraform/aws/node
    ```

3. Initialize Terraform:
    ```bash
    terraform init
    ```

4. Plan the Terraform execution:
    ```bash
    terraform plan
    ```

5. Apply the Terraform configuration:
    ```bash
    terraform apply
    ```
    You will be prompted to enter values for the variables if not provided.

6. The Ansible playbook will run automatically after the cloud resources are created.

7. To destroy the created resources when you're done:
    ```bash
    terraform destroy
    ```

## One-step Execution

You can also run the entire process in one step by providing all variable values in the command line. For AWS Node.js deployment:

```bash
terraform apply -auto-approve \
-var="access_key=<YOUR_AWS_ACCESS_KEY>" \
-var="secret_key=<YOUR_AWS_SECRET_KEY>" \
-var="region=<AWS_REGION>" \
-var="key_name=<PEM_FILE.pem>" \
-var="instance_type=<AWS_INSTANCE_TYPE>" \
-var="ami_id=<AWS_AMI_ID_FOR_SELECTED_ZONE>" \
-var="instance_name=<INSTANCE_NAME>"
```
Replace the placeholders (enclosed in <>) with your actual values.

## Ansible Configuration

The Ansible playbook (`playbook.yml`) performs framework-specific tasks. For the AWS Node.js setup, it:

1. Installs Node.js and npm
2. Clones a specified Git repository containing a Node.js application
3. Installs application dependencies
4. Sets up and starts the application using PM2

You can modify the Ansible playbook to suit your specific deployment needs.

### Notes
- The private key for SSH access will be saved in the current directory with the name specified in `key_name`. Ensure to keep this file secure and do not commit it to version control.
- For AWS Node.js deployments, the application will be accessible at `http://<INSTANCE_PUBLIC_IP>:3000` after deployment.
- Ensure your cloud provider credentials have the necessary permissions to create the required resources.
- The structure allows for easy addition of new cloud providers and frameworks. Simply add new directories under the respective provider folder and include the necessary Terraform and Ansible files.