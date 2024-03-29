**Using STS to Assume a Role**

- Define an IAM Role within your account or cross-account
- Define which principals can access this IAM Role
- Use AWS STS (Security Token Service) to retrieve credentials and impersonate the IAM Role you have access to (AssumeRole API)
- Temporary credentials can be valid between 15 minutes to 12 hour

**Assuming a Role with STS**

- Provide access for an IAM user in one AWS account that you own to access resources in another account that you own
- Provide access to IAM users in AWS accounts owned by third parties
- Provide access for services offered by AWS to AWS resources
- Provide access for externally authenticated users (identity federation)
- Ability to revoke active sessions and credentials for a role
(by adding a policy using a time statement – AWSRevokeOlderSessions)
- **When you assume a role (user, application or service), you give up your original permissions and take the permissions assigned to the role**

- You must explicitly grant your users permission to assume the role.
- Your users must actively switch to the role using the AWS Management Console or assume the role using the AWS CLI or AWS API
- You can add multi-factor authentication (MFA) protection to the role so that only users who sign in with an MFA device can assume the role
- Least privilege + auditing using CloudTrail

**Resolve Confused Deputy**

- If providing access to AWS accounts owned by Third Parties 
- add external id 
- add session tag

**STS Important APIs**

- **AssumeRole**: access a role within your account or cross-account
- **AssumeRoleWithSAML**: return credentials for users logged with SAML
- **AssumeRoleWithWebIdentity**: return creds for users logged with an IdP
- Example providers include Amazon Cognito, Login with Amazon, Facebook, Google, or any OpenID Connect-compatible identity provider
- AWS recommends using Cognito instead
- **GetSessionToken**: for MFA, from a user or AWS account root user
- **GetFederationToken**: obtain temporary creds for a federated user, usually a proxy app that will give the creds to a distributed app inside a corporate network
