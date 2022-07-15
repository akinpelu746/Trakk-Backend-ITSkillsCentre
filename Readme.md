Before deploying into any account, we need to to set up backend infarstructure for tracking state file. To do so, follow the following instructions:

- `cd backend` firectory
- update the main.auto.tfars
- Run terraform   `terraform init`to intialize your directory and then `terrfaorm plan` to get the plan of the changes that terraform will
- `terraform apply` will create s3 for storing state file, a second s3 for logging and dynamo db for locking state files.
-  The generated files can be commited to source control for tracking
-  Take note of the bucket and dynamo db generated,


The __001SSM folder is to deploy SSM  run which installed inspector agents on all the ec2 instances.
Take Note of the following before deploying the ssm, the window target is all the ec2 instances in the account. This can be changed to filter the ec2 through tag on [line 18](./__01SSM/main.tf)

- cd to the _01SSM directory
- Fill the backend.tf with values gotten from the backend_directory, the `key` value is the name of the file to be used in the bucket
- Fill the auto.tfvars
- Run terraform   `terraform init`to intialize your directory and then `terrfaorm plan` to get the plan of the changes that terraform will
- `terraform apply` will  windows target and windows maintenace and windows task to run on the targets, cloudwatch group for the logs.


The __002inspector folder is to deploy inspector. The inspector rules is triggered using event bridge.
- cd to the _002inspector directory
- Fill the backend.tf with values gotten from the backend_directory, the `key` value is the name of the file to be used in the bucket
- Fill the auto.tfvars
- Run terraform   `terraform init`to intialize your directory and then `terrfaorm plan` to get the plan of the changes that terraform will
- `terraform apply` will  deploy inspcetor and create event bridge to trigger the rules.
