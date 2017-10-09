# ECR
Creates the ECR repository for each service.

For each `service` you will need to create a `AWS::ECR::Repository` within the cloudformation.yml.

The `Service1RepositoryUrl` output parameter is used when service docker images.  An image is required prior to deploying the `ecs` stack.