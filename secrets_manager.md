### AWS Secrets Manager

- Meant for storing secrets (e.g., passwords, API keys, ...)
- Capability to force rotation of secrets every X days
- Automate generation of secrets on rotation (uses Lambda)
- Natively supports Amazon RDS (all supported DB engines), Redshift, DocumentDB
- Support other databases and services (custom Lambda function)
- Control access to secrets using Resource-based Policy
- Integration with other AWS services to natively pull secrets from Secrets Manager: CloudFormation, CodeBuild, ECS, EMR, Fargate, EKS, Parameter Store...

### SSM Parameter Store vs Secrets Manager

- Secrets Manager ($$$):
  - Automatic rotation of secrets with AWS Lambda
  - Lambda function is provided for RDS, Redshift, DocumentDB • KMS encryption is mandatory
  - Can integration with CloudFormation
- SSM Parameter Store ($):
  - Simple API
  - No secret rotation (can enable rotation using Lambda triggered by EventBridge)
  - KMS encryption is optional
  - Can integration with CloudFormation
  - Can pull a Secrets Manager secret using the SSM Parameter Store API
