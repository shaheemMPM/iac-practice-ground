# EC2 Instance Terraform Configuration

This Terraform configuration creates an EC2 instance in AWS along with a new key pair for SSH access.

## What it does

1. Creates a new RSA key pair
2. Saves the private key to a local file
3. Creates an EC2 instance with specified AMI and instance type
4. Tags the instance with a provided name
5. Outputs the public IP of the created instance

## Prerequisites

- Terraform installed on your local machine
- AWS account with appropriate permissions
- AWS CLI configured with your credentials (optional)

## Usage

1. Clone this repository or copy the `main.tf` and `variables.tf` files to your local machine.

2. Initialize Terraform:
    ```bash
    terraform init
    ```

3. Plan the Terraform execution to see what resources will be created:
    ```bash
    terraform plan
    ```

4. Apply the Terraform configuration to create the resources:
    ```bash
    terraform apply
    ```
    You will be prompted to enter values for the variables if not provided.

5. To destroy the created resources when you're done:
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

### Note
The private key for SSH access will be saved in the current directory with the name specified in `key_name`. Ensure to keep this file secure and do not commit it to version control.