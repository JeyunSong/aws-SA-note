### AWS Organizations - Organization Account Access Role

- IAM role which grants full administrator permissions in the Member account to the Management account
- Used to perform admin tasks in the Member accounts (e.g., creating IAM users)
- Could be assumed by IAM users in the Management account
- Automatically added to all new Member accounts created with AWS Organizations
- Must be created manually if you invite an existing Member account

### Multi Account Strategies

- Create accounts per department, per cost center, per dev / test / prod, based on regulatory restrictions (using SCP), for better resource isolation (ex:VPC), to have separate per-account service limits, isolated account for logging
- Multi Account vs. One Account Multi VPC
- Use tagging standards for billing purposes
- Enable CloudTrail on all accounts, send logs to central S3 account
- Send CloudWatch Logs to central logging account
- Strategy to create an account for security

### AWS Organization - Feature Modes

- Consolidated billing features:
- Consolidated Billing across all accounts - single payment method
- Pricing benefits from aggregated usage (volume discount for EC2, S3...)
- All Features (Default):
- Includes consolidated billing features, SCP
- Invited accounts must approve enabling all features
- Ability to apply an SCP to prevent member accounts from leaving the org
- Can’t switch back to Consolidated Billing Features only

### AWS Organizations – Reserved Instances

- For billing purposes, the consolidated billing feature of AWS Organizations treats all the accounts in the organization as one account.
- This means that all accounts in the organization can receive the hourly cost benefit of Reserved Instances that are purchased by any other account.
- The payer account (Management account) of an organization can turn off Reserved Instance (RI) discount and Savings Plans discount sharing for any accounts in that organization, including the payer account
- This means that RIs and Savings Plans discounts aren't shared between any accounts that have sharing turned off.
- To share an RI or Savings Plans discount with an account, both accounts must have sharing turned on

### AWS Organizations – Moving Accounts

1. Remove the member account from the AWS Organization
2. Send an invite to the member account from the AWS Organization
3. Accept the invite to the new Organization from the member account

### Service Control Policies (SCP)

- Define allowlist or blocklist IAM actions
- Applied at the OU or Account level
- Does not apply to the Management Account
- SCP is applied to all the Users and Roles in the account, including Root user
- The SCP does not affect Service-linked roles
- Service-linked roles enable other AWS services to integrate with AWS Organizations and can't be restricted by SCPs.
- SCP must have an explicit Allow (does not allow anything by default)
- Use cases:
- Restrict access to certain services (for example: can’t use EMR)
- Enforce PCI compliance by explicitly disabling services

### Restricting Tags with IAM Policies

- You can restrict specific Tags on AWS resources
- Using the aws:TagKeys Condition Key
- Validate the Tag Keys attached to a resource against the Tag Keys in the IAM Policy
- Example: allow IAM users to create EBS Volumes only if it has the “Env” and “CostCenter” Tags
- Use either ForAllValues (must have all keys) or ForAnyValue (must have any of these keys at a minimum)

AWS Organizations – Tag Policies

- Helps you standardize tags across resources in an AWS Organization
- Ensure consistent tags, audit tagged resources, maintain proper resources categorization, ...
- You defineTag keys and their allowed values
- Helps with AWS Cost Allocation Tags and Attribute-based Access Control
- Prevent any non-compliant tagging operations on specified services and resources
- Generate a report that lists all tagged/non- compliant resources
- Use Amazon EventBridge to monitor non- compliant tags

### AWS Organizations – AI Services Opt-out Policies

- Certain AWS AI services may use your content for continuous improvement of Amazon AI/ML services
- Example: Amazon Lex, Amazon Comprehend, Amazon Polly, ...
- You can opt-out of having your content stored or used by AWS AI services
- Create an Opt-out Policy that enforces this setting across all Member accounts and AWS Regions All Services
- You can opt-out all AI services or selected services
- Can be attached to Organization Root, specific OU, or individual Member account

### AWS Organizations – Backup Policies

- AWS Backup enables you to create Backup Plans that define how to backup your AWS resources
- JSON documents that define Backup Plans across an AWS Organization
- Gives you granular control over backing up your resources (e.g., backup frequency, time window, backup region, ...)
- Can be attached to Organization Root, specific OU, or individual Member account
- Immutable Backup Plans appear in Member accounts (view ONLY)

[AWS Organizations란 무엇인가요? - AWS Organizations](https://docs.aws.amazon.com/ko_kr/organizations/latest/userguide/orgs_introduction.html)
