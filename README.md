# CIM's Services Stack
Quickly deploy Microservices with ECS and CloudFormation.

Example:
- `https://example.com/service1`
- `https://example.com/service2`

This quickstart is based off:
- https://aws.amazon.com/quickstart/architecture/vpc/
- https://github.com/awslabs/ecs-refarch-cloudformation

[![](architecture.png)](architecture.png)

# Setup
## Prerequisites 
- Install `cim` https://cim.sh
- Register your domain with Route53
- Or point your existing domain to Route53
- Configure 'admin@yourdomain.com' to receive the SSL verification email
  - You will have to confirm this email address.  This is annoying and I've asked AWS to remove this step if the domain is used with Route53.
  
## Stack Up
