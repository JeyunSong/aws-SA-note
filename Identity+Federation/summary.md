### Summary

- Users and Accounts all in AWS
- AWS Organizations
- AWS Control Tower to setup secure & complaint multi-account AWS environment (best practices)
- Federation with SAML
- Federation without SAML with a custom IdP (GetFederationToken)
- AWS Single Sign-On to connect to multiple AWS Accounts (Organization) and SAML apps
- Web Identity Federation (not recommended)
- Cognito for most web and mobile applications (has anonymous mode, MFA)
- AWS Directory Service:
  - Managed Microsoft AD – standalone or setup trust AD with on-premises, has MFA, seamless join, RDS

### integration

- AD Connector – proxy requests to on-premises
- Simple AD – standalone & cheap AD-compatible with no MFA, no advanced capabilities
- AWS RAM to share resources (example VPC subnets)