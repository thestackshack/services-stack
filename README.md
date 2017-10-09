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
### VPC
Launch the VPC stack first.
```
cd vpc
cim stack-up
```
### ECR
Launch the AWS docker image registry next.
```
cd service/ecr
cim stack-up
```
### ECS
Launch the AWS ECS cluster next.
```
cd service/ecs
cim stack-up
```
### service1

Before we can launch this cloudformation stack.  We need to push our service image to ECR.
#### Push Image
- [Registry Authentication](http://docs.aws.amazon.com/AmazonECR/latest/userguide/Registries.html#registry_auth)
  - `aws ecr get-login --registry-ids <account-id>`
  - copy/past output to perform docker login,  also append `/services-stack/service1` to the repository url.
- Build Image
  - `docker build -t service1:<version> .`
- [Push Image](http://docs.aws.amazon.com/AmazonECR/latest/userguide/docker-push-ecr-image.html)
  - `docker tag service1:<version> <account-id>.dkr.ecr.<region>.amazonaws.com/services-stack/service1`
  - `docker tag service1:<version> <account-id>.dkr.ecr.<region>.amazonaws.com/services-stack/service1:<version>`
  - `docker push <account-id>.dkr.ecr.<region>.amazonaws.com/services-stack/service1`

#### Update Version
Make sure the `Version` parameter, in _cim.yml, matches the `version` tag from above.  The ECS Task Definition will pull the image from ECR.

#### Stack up
Once the `Version` is set you can use `cim stack-up` to update the stack with the new version.

```
cd service/service1
cim stack-up
```