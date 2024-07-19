# Kubecloud

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
