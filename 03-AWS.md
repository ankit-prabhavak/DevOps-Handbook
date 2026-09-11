# AWS CLI for DevOps with Advanced Querying & Filtering

## Initial Setup & Identity

Configure AWS CLI credentials, default region, and output format interactively:
```bash
aws configure
```

Verify the currently authenticated AWS IAM user or role and Account ID:
```bash
aws sts get-caller-identity
```

Extract only the AWS Account ID string from the identity payload:
```bash
aws sts get-caller-identity --query "Account" --output text
```

Extract only the ARN string of the active user or role:
```bash
aws sts get-caller-identity --query "Arn" --output text
```

## EC2 (Elastic Compute Cloud)

List all EC2 instances and their metadata in the configured region:
```bash
aws ec2 describe-instances --output table
```

Connect to a remote EC2 Linux instance securely using an SSH private key:
```bash
ssh -i key.pem ec2-user@IP
```

List only running EC2 instances with specific filters:
```bash
aws ec2 describe-instances --filters "Name=instance-state-name,Values=running" --query "Reservations[*].Instances[*].[InstanceId,PublicIpAddress]" --output table
```

Query the public IP address of an instance by passing its specific Name tag:
```bash
aws ec2 describe-instances --filters "Name=tag:Name,Values=Prod-Webserver" --query "Reservations[*].Instances[*].PublicIpAddress" --output text
```

List all Instance IDs along with their current lifecycle state:
```bash
aws ec2 describe-instances --query "Reservations[*].Instances[*].[InstanceId,State.Name]" --output table
```

Start a specific EC2 instance:
```bash
aws ec2 start-instances --instance-ids i-0123456789abcdef0
```

Stop a specific running EC2 instance:
```bash
aws ec2 stop-instances --instance-ids i-0123456789abcdef0
```

## S3 (Simple Storage Service)

List all S3 buckets in the AWS account:
```bash
aws s3 ls
```

List the contents of a specific S3 bucket:
```bash
aws s3 ls s3://bucket-name
```

Use the api-level query to isolate and print only bucket names matching a clean list format:
```bash
aws s3api list-buckets --query "Buckets[*].Name" --output table
```

Upload a local file to a specific S3 bucket:
```bash
aws s3 cp backup.sql s3://bucket-name
```

Download a file from an S3 bucket to the current local directory:
```bash
aws s3 cp s3://bucket-name/file .
```

Synchronize a local directory with an S3 bucket (only copies new or changed files):
```bash
aws s3 sync ./local-folder s3://bucket-name/remote-folder
```

Remove an object from an S3 bucket:
```bash
aws s3 rm s3://bucket-name/file.txt
```

## IAM (Identity and Access Management)

List all IAM users in the AWS account:
```bash
aws iam list-users
```

Isolate and extract only user names from the user directory:
```bash
aws iam list-users --query "Users[*].UserName" --output table
```

List all IAM groups in the account:
```bash
aws iam list-groups
```

List the IAM policies attached to a specific user:
```bash
aws iam list-attached-user-policies --user-name john.doe
```

## ECR (Elastic Container Registry)

Authenticate the local Docker daemon with an AWS ECR registry:
```bash
aws ecr get-login-password --region ap-south-1 | docker login --username AWS --password-stdin ACCOUNT_://amazonaws.com
```

Create a new private container repository in ECR:
```bash
aws ecr create-repository --repository-name myapp --region ap-south-1
```

List all container images stored within a specific ECR repository:
```bash
aws ecr list-images --repository-name myapp
```

Query only the image tags present inside a repository to inspect deployments:
```bash
aws ecr list-images --repository-name myapp --query "imageIds[*].imageTag" --output table
```

## CloudWatch & Logs

List all CloudWatch log groups in the region:
```bash
aws logs describe-log-groups
```

Query and list only the names of the log groups:
```bash
aws logs describe-log-groups --query "logGroups[*].logGroupName" --output table
```

List the log streams inside a specific CloudWatch log group:
```bash
aws logs describe-log-streams --log-group-name /aws/lambda/my-function
```

Retrieve the latest log events from a specific CloudWatch log stream:
```bash
aws logs get-log-events --log-group-name /aws/containerinsights/cluster/application --log-stream-name stream-id --limit 50
```

## SNS (Simple Notification Service)

List all SNS topics created in the account:
```bash
aws sns list-topics
```

Query and extract only the Amazon Resource Names (ARNs) of your SNS topics:
```bash
aws sns list-topics --query "Topics[*].TopicArn" --output table
```

Publish a plain-text message directly to an SNS topic:
```bash
aws sns publish --topic-arn arn:aws:sns:ap-south-1:123456789012:MyTopic --message "Deployment Successful"
```

List all active subscriptions for SNS topics:
```bash
aws sns list-subscriptions
```
