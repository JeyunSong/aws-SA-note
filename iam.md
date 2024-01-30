## IAM


**Users & Groups**

- Identity and Access Management, Global service
- Root account created by default, shouldn’t be used or shared
- Users are people within your organization, and can be grouped
- Groups only contain users, not other groups
- Users don’t have to belong to a group, and user can belong to multiple groups

**Permissions**

- Users or Groups can be assigned JSON documents called policies
- These policies define the permissions of the users
- In AWS you apply the least privilege principle: don’t give more permissions than a user needs

**Policies Structure** 

- Consists of 
  - Version : policy language cersion, always include "2012-10-17"
  - Id : an identifier for the policy (optional)
  - Statement : one or more individual statements (required)
- Statements consists of
  - Sid : an identifier for the statement (optional)
  - Effect : whether the statement allows or denies access (Allow, Deny)
  - Principal : account/user/role to which this policy applied to
  - Action : list of actions this policy allows or denies
  - Condition : conditions for when this policy is in effect (optional)

 ~~~
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
      "Resource": ["arn:aws:s3::jeyunbucket/*"]
    }
  ]
}
~~~


**Access options** 

- AWS Management Console : protected by password + MFA(Multi Factor Authentication)
- AWS Command Line Interface (CLI) : protected by access keys
- AWS Software Developer Kit (SDK) - for code : protected by access keys

**MFA**

- password you know + security device you own
- if a password is stolen or hacked, the account is not compromised
- Option_1 : Virtual MFA device (Google Authenticator, Authy)
- Option_2 : Physical MFA device (U2F, Key Fob Device)

**Security Tools**

- IAM Credentials Report : account-level
- a report that lists all your account’s users and status of their various credentials
- IAM Access Advisor : user-level
- Access advisor shows the service permissions granted to a user and when those services were last accessed
- You can use this information to revise your policies
