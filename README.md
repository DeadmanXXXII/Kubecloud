# Kubecloud


---

Security Report: Combination Attack on AWS Infrastructure


---

Summary

This report details a combination attack using stolen AWS keys to access and control AWS infrastructure. The initial vector is a malicious PyPI package that exfiltrates AWS credentials called fabrice, and the second vector is utilizing these keys to run infrastructure provisioning scripts, like the KubeCloudV2.sh script found on the GitHub repository.

Attack Scenario

1. Stage 1: AWS credentials are stolen via a malicious PyPI package fabrice.

2. Stage 2: The stolen AWS keys are used to execute infrastructure provisioning scripts (KubeCloudV2.sh), which deploy resources and services in the AWS environment, potentially including EC2 instances and Kubernetes-managed applications like MinIO.




---

CVE & CWE Information

CWE-798: Use of Hard-coded Credentials
Description: Hard-coded credentials or API keys are embedded in infrastructure automation scripts.

CWE-522: Insufficiently Protected Credentials
Description: Storing credentials in unsecured locations (e.g., configuration files without encryption).

CWE-352: Cross-Site Request Forgery (CSRF)
Description: The lack of protections when executing actions that require user credentials, such as API key exfiltration, can lead to CSRF attacks.

CWE-295: Improper Certificate Validation
Description: If communications with AWS services are not properly secured, the attacker could intercept API requests and responses.



---

CVSS Score Breakdown for Combination Attack on AWS Infrastructure:

Base Score: 9.1 (Critical)

Attack Vector:

Network: Exploitable over the network. The attack leverages stolen AWS keys that can be used remotely to control AWS infrastructure.


Attack Complexity:

Low: The attack is straightforward once the keys are compromised. It does not require special conditions or advanced techniques.


Privileges Required:

Low: Minimal privileges are needed initially, as the attacker only requires stolen AWS keys to begin exploiting the system.


User Interaction:

None: The attack does not depend on any legitimate user’s actions, allowing the attacker to act autonomously.


Scope:

Changed: The attack impacts multiple AWS components and services. A successful breach of one system extends to other parts of the AWS environment.


Confidentiality Impact:

High: Compromised credentials allow access to sensitive data within AWS, putting data confidentiality at serious risk.


Integrity Impact:

High: The attacker can modify, deploy, or destroy resources, affecting the integrity of the AWS environment.


Availability Impact:

High: Unauthorized infrastructure provisioning can lead to resource exhaustion, potential service disruptions, and a loss of availability for legitimate users.


Final CVSS Score: 9.1 (Critical)


---

Reproduction Steps

To simulate and reproduce the attack:

1. Deploy the Malicious PyPI Package

Use the PyPI package fabrice's h0nda described in the Bleeping Computer article.


https://www.bleepingcomputer.com/news/security/malicious-pypi-package-with-37-000-downloads-steals-aws-keys/amp/

Install the package in a test environment, and observe the exfiltration of AWS credentials.



2. Steal AWS Keys

Confirm that the fabrice package exfiltrates AWS credentials by monitoring network traffic and identifying unauthorized external connections.



3. Run KubeCloudV2.sh with Stolen Keys

Use the compromised keys to execute the KubeCloudV2.sh script.

Run the script to provision an AWS instance and deploy MinIO, as defined in the terraform/main.tf and minio-deployment.yaml configurations.



4. Observe the Provisioned Infrastructure

Verify that AWS resources, such as EC2 instances, are created.

Check that MinIO is deployed and accessible, potentially exposing stored data.

---

Impact

The stolen AWS keys allow the attacker to:

Provision AWS Resources: Unauthorized EC2 instances can lead to unexpected charges, security risks, and potential data exfiltration.

Deploy Applications (MinIO): Unauthorized deployments can result in unauthorized data storage and exposure, with the attacker gaining full control over MinIO storage.

Alter or Destroy Infrastructure: Malicious scripts could terminate or modify resources, impacting the availability and integrity of the AWS environment.

Data Exfiltration: MinIO or other deployed services could be used to store and exfiltrate sensitive data, impacting confidentiality.

---

Mitigations

1. Credential Security

Rotate AWS credentials regularly and avoid storing them in plaintext within scripts or configuration files.

Use IAM roles and instance profiles to manage permissions securely.



2. Monitoring and Detection

Set up monitoring for unusual API activity and use AWS CloudTrail to track access patterns.

Implement GuardDuty for continuous threat detection and automated response.



3. Vulnerability Scanning and Dependency Management

Regularly scan for malicious dependencies in project dependencies and restrict the use of untrusted libraries.

Use tools like AWS Inspector for vulnerability assessments and dependency analysis.



4. Implement Least Privilege Policies

Restrict permissions for AWS resources to only those necessary for functionality, minimizing impact if credentials are compromised.

---

Additional Recommendations

Use AWS Secrets Manager for secure storage of credentials.

Regularly audit infrastructure-as-code scripts to remove any hard-coded credentials.

Apply restrictive network policies for resources deployed by infrastructure automation to limit unauthorized access.


![Attck PoC in terminal.](https://raw.githubusercontent.com/DeadmanXXXII/Kubecloud/main/Screenshot_20240625-204258.png)

---



Walkthrough of Each Option and What It Can Do
 
Option 1: 

Provision InfrastructureFunction: provision_infrastructure()Description: Initiates the provisioning of cloud infrastructure using Terraform.
Actions:
Generates a Terraform configuration (main.tf) for provisioning an AWS EC2 instance (t2.micro in us-west-2 region).
Initializes Terraform and applies the configuration to provision the infrastructure.Usage: 
Select option 1 from the main menu and follow prompts to confirm and initiate infrastructure provisioning.

Option 2: 

Manage UsersFunction: manage_users()Description: 
Provides user management functionalities.
Actions:
Offers options to create or delete user accounts.Calls respective functions (create_user() and delete_user()) based on user input.
Usage:
Select option 2 from the main menu.

Sub-options:

Option 1: 
Create User (create_user()):Prompts for username and simulates creation of a user.

Option 2: 
Delete User (delete_user()):Prompts for username to delete and simulates deletion of a user.


Option 3: 

Transfer FilesFunction: transfer_files()Description: 
Facilitates file transfer operations (upload and download).

Actions:
Offers options to upload or download files using zenity for file selection dialogs.
Calls respective functions (upload_file() and download_file()) based on user input.

Usage: 
Select option 3 from the main menu:

Sub-options:

Option 1: 
Upload File (upload_file()):
Opens a file selection dialog (zenity) to choose a file to upload.Simulates uploading the selected file.

Option 2: 
Download File (download_file()):
Opens a file selection dialog (zenity) to choose a location to save a file.
Simulates downloading a file to the selected location.

Option 4: 

Deploy MinIOFunction: deploy_minio()Description: 

Deploys MinIO, a cloud-native object storage server, using Kubernetes.

Actions:
Generates a Kubernetes Deployment YAML (minio-deployment.yaml) to deploy MinIO with specified configurations.
Applies the YAML using kubectl to deploy MinIO in the Kubernetes cluster.

Usage: 
Select option 4 from the main menu to deploy MinIO.Details:
Configures MinIO with access and secret keys (MINIO_ACCESS_KEY and MINIO_SECRET_KEY).
Deploys MinIO as a single replica with port 9000 exposed for object storage operations.

Option 5: 

ExitDescription: 
Exits the script gracefully.
Usage: 
Select option 5 from the main menu to exit the script.
Conclusion 
The kubecloud.sh script provides a comprehensive set of functionalities for managing cloud infrastructure, user accounts, file transfers, and deploying MinIO using Kubernetes. Each option is designed to simulate basic operations and interactions within a cloud management system, demonstrating essential tasks and their implementation in a scripted environment.

Examples of usage:

Example 1: 
Deploy MinIO and Manage UsersDeploy MinIOSelect option 4 from the main menu to deploy MinIO using Kubernetes.
Follow the prompts to deploy MinIO with specified access and secret keys.
Manage UsersSelect option 2 from the main menu to manage users.
Choose option 1 to create a new user and enter a username.
Choose option 2 to delete an existing user and enter the username to delete.

Example 2: 
Provision Infrastructure and Transfer FilesProvision InfrastructureSelect option 1 from the main menu to provision infrastructure using Terraform.
Follow the prompts to confirm and initiate the provisioning of an AWS EC2 instance.
Transfer FilesSelect option 3 from the main menu to transfer files.
Choose option 1 to upload a file using a file selection dialog (zenity).
Choose option 2 to download a file to a specified location using a file selection dialog.

Example 3: 
Manage Users and Deploy MinIOManage UsersSelect option 2 from the main menu to manage users.
Choose option 1 to create a new user and enter a username.
Choose option 2 to delete an existing user and enter the username to delete.
Deploy MinIOSelect option 4 from the main menu to deploy MinIO using Kubernetes.
Follow the prompts to deploy MinIO with specified access and secret keys.

Example 4: 
Transfer Files and Provision InfrastructureTransfer FilesSelect option 3 from the main menu to transfer files.Choose option 1 to upload a file using a file selection dialog (zenity).
Choose option 2 to download a file to a specified location using a file selection dialog.
Provision InfrastructureSelect option 1 from the main menu to provision infrastructure using Terraform.
Follow the prompts to confirm and initiate the provisioning of an AWS EC2 instance.

Example 5: 
Random Sequence of ActionsDeploy MinIOSelect option 4 from the main menu to deploy MinIO using Kubernetes.
Follow the prompts to deploy MinIO with specified access and secret keys.
Transfer Files Select option 3 from the main menu to transfer files.
Choose option 1 to upload a file using a file selection dialog (zenity).
Choose option 2 to download a file to a specified location using a file selection dialog.
Manage UsersSelect option 2 from the main menu to manage users.
Choose option 1 to create a new user and enter a username.
Choose option 2 to delete an existing user and enter the username to delete.

Conclusion: 
These examples showcase the versatility of the kubecloud.sh script, allowing you to perform various cloud management tasks such as provisioning infrastructure, deploying applications (MinIO), managing users, and transferring files. 
You can mix and match these functionalities based on your operational needs within a Kubernetes environment, demonstrating the script's capabilities in different scenarios.
