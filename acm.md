### AWS Certificate Manager (ACM)

- To host public SSL certificates in AWS, you can:
- Buy your own and upload them using the CLI
- Have ACM provision and renew public SSL certificates for you (free of cost)
- ACM loads SSL certificates on the following integrations:
- Load Balancers (including the ones created by EB) • CloudFront distributions
- APIs on API Gateways
- SSL certificates is overall a pain to manually manage, so ACM is great to leverage in your AWS infrastructure!

### ACM – Good to know

- Possibility of creating public certificates
  - Must verify public DNS
  - Must be issued by a trusted public certificate authority (CA)
- Possibility of creating private certificates
  - For your internal applications
  - You create your own private CA
  - Your applications must trust your private CA
- Certificate renewal:
  - Automatically done if generated provisioned by ACM
  - Any manually uploaded certificates must be renewed manually and re-uploaded
- ACM is a regional service
  - To use with a global application (multiple ALB for example), you need to issue an SSL certificate in each region where you application is deployed.
  - You cannot copy certs across regions
