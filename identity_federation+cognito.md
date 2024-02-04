### Identity Federation in AWS

- Give users outside of AWS permissions to access AWS resources in your account
- You don’t need to create IAM Users (user management is outside AWS)
- Use cases:
- A corporate has its own identity system (ex. Active Directory) 
- Web/Mobile application that needs access to AWS resources
- Identity Federation can have many flavors: 
- SAML 2.0
- Custom Identity Broker
- Web Identity Federation With(out) Amazon Cognito
- Single Sign-On (SSO)

### SAML 2.0 Federation

- Security Assertion Markup Language 2.0 (SAML 2.0)
- Open standard used by many identity providers (e.g.,ADFS)
- Supports integration with Microsoft Active Directory Federations Services(ADFS)
- Or any SAML2.0 – compatible IdPs with AWS
- Access to AWS Console, AWS CLI, or AWS API using temporary credentials
- No need to create IAM Users for each of your employees
- Need to setup a trust between AWS IAM and SAML 2.0 Identity Provider (both ways)
- Under-the-hood: Uses the STS API AssumeRoleWithSAML
- SAML 2.0 Federation is the “old way”, Amazon Single Sign-On (AWS SSO) Federation is the new managed and simpler way
- Ref.
    
    [Enabling Federation to AWS Using Windows Active Directory, ADFS, and SAML 2.0 | Amazon Web Services](https://aws.amazon.com/ko/blogs/security/enabling-federation-to-aws-using-windows-active-directory-adfs-and-saml-2-0/)
    

### Custom Identity Broker Application

- Use only if Identity Provider is NOT compatible with SAML 2.0
- The Identity Broker Authenticates users & requests temporary credentials from AWS
- The Identity Broker must determine the appropriate IAM Role
- Uses the STS API AssumeRole or GetFederationToken

### Web Identity Federation - With Cognito

- Preferred over for Web Identity Federation
- Create IAM Roles using Cognito with the least privilege needed
- Build trust between the OIDC IdP and AWS
- Cognito benefits:
- Supports anonymous users • Supports MFA
- Data Synchronization
- Cognito replaces a Token Vending Machine (TVM)
- Without Cognito is not recommended now

### **Web Identity Federation – IAM Policy**

- After being authenticated with Web Identity Federation, you can identify the user with an IAM policy variable
- Examples:
- cognito-identity.amazonaws.com:sub
- amazon.com:user_id
- graph.facebook.com:id
- accounts.google.com:sub
