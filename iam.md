## **IAM**

**IAM Users & Groups**

- Identity and Access Management, Global service
- Root account created by default, shouldn’t be used or shared
- Users are people within your organization, and can be grouped
- Groups only contain users, not other groups
- Users don’t have to belong to a group, and user can belong to multiple groups

**IAM Permissions**

- Users or Groups can be assigned JSON documents called policies
- These policies define the permissions of the users
- In AWS you apply the least privilege principle: don’t give more permissions than a user needs

**IAM Policies**

- Anatomy of a policy : JSON doc with effect, Action, Resource, Conditions, Policy Variables
- Explicit deny has precedence over allow
- Best practice : use least privilege for maximum security
- Access advisor : see permissions granted and when last accessed
- Access Analyzer : analyze resources that are shared with external entity

**IAM Policies Structure**

- Consists of
    - Version : policy language version, always include "2012-10-17"
    - Id : an identifier for the policy (optional)
    - Statement : one or more individual statements (required)
- Statements consists of
    - Sid : an identifier for the statement (optional)
    - Effect : whether the statement allows or denies access (Allow, Deny)
    - Principal : account/user/role to which this policy applied to
    - Action : list of actions this policy allows or denies
    - Condition : conditions for when this policy is in effect (optional)

```
{
 "Version": "2012-10-17",
 "id" : "S3-Account-Permissions",
 "Statement": [
   {
     "Sid" : "1",
     "Effect": "Allow",
     "Principal" : {
       "AWS" : ["arn:aws:iam::00000000:root"]
     },
     "Action": [
       "s3:GetObject",
       "s3:PutObject"
     ],
     "Resource": "arn:aws:s3::jeyunbucket/*",
		 "Condition": {
          "NumericLessThanEquals": {"aws:MultiFactorAuthAge": "3600"}
      }
   }
 ]
}

```

**IAM Condition Operatiors**

- String : StringEquals, StringNotEquals, StringLike, …
- Numeric : NumericEquals, NumericNotEquals, NumericLessThen, …
- Date : DateEquals, DateNotEquals, DateLessThan
- Boolean : Bool
- IpAdress
- ArnEquals, ArnLike
- Null

**IAM Roles vs Resource Based Policies**

- When you assume a role (user, application or service), you give up your original permissions and take the permissions assigned to the role
- When using a resource-based policy, the principal doesn’t have to give up any permissions
- Example: User in account A needs to scan a DynamoDB table in Account A and dump it in an S3 bucket in Account B.
- Supported by: Amazon S3 buckets, SNS topics, SQS queues, Lambda functions, ECR, Backup, EFS, Glacier, Cloud9, AWS Ar tifact, Secrets Manager, ACM, KMS, CloudWatch Logs, API Gateway, EventBridge etc...

**IAM Permission Boundaries**

- Can be used in combinations of AWS organization SCP

**IAM Access Analyzer Policy Validation**

- Validates your policy against IAM policy grammar and best practices
- General warning, security warnings, errors, suggestions
- Provides actionable recommendations

**IAM Access Analyzer Policy Generation**

- Generates IAM policy based on access activity
- CloudTrail logs is reviewed to generate the policy with the fine-grained permissions and the appropriate Actions and Services
- Reviews CloudTrail log for up to 90 days

**AWS Account Access options** 

- AWS Management Console : protected by password + MFA
- AWS Command Line Interface (CLI) : protected by access keys
- AWS Software Developer Kit (SDK) - for code : protected by access keys

**MFA (Multi Factor Authentication))**

- password you know + security device you own
- if a password is stolen or hacked, the account is not compromised
- Option(1) : Virtual MFA device (Google Authenticator, Authy)
- Option(2) : Physical MFA device (U2F, Key Fob Device)  as

**IAM Security Tools**

- IAM Credentials Report : account-level
- a report that lists all your account’s users and status of their various credentials
- IAM Access Advisor : user-level
- Access advisor shows the service permissions granted to a user and when those services were last accessed
- You can use this information to revise your policies

## Reference

[IAM 엔터티의 권한 범위 - AWS Identity and Access Management](https://docs.aws.amazon.com/ko_kr/IAM/latest/UserGuide/access_policies_boundaries.html)

[IAM 자격 증명 기반 정책의 예 - AWS Identity and Access Management](https://docs.aws.amazon.com/ko_kr/IAM/latest/UserGuide/access_policies_examples.html)

[IAM의 정책 및 권한 - AWS Identity and Access Management](https://docs.aws.amazon.com/ko_kr/IAM/latest/UserGuide/access_policies.html#inline)

[IAM의 임시 보안 자격 증명 - AWS Identity and Access Management](https://docs.aws.amazon.com/ko_kr/IAM/latest/UserGuide/id_credentials_temp.html)

[자격 증명 기반 정책 및 리소스 기반 정책 - AWS Identity and Access Management](https://docs.aws.amazon.com/ko_kr/IAM/latest/UserGuide/access_policies_identity-vs-resource.html)

[IAM의 크로스 계정 리소스 액세스 - AWS Identity and Access Management](https://docs.aws.amazon.com/ko_kr/IAM/latest/UserGuide/access_policies-cross-account-resource-access.html)
