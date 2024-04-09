# Topic 4 - Docker image website(service) with Database connetion

###### Yuanchao Hands-on Project

###### Check this doc and project template on Github  [here](https://github.com/lyc-handson-aws/handson-topic5)

## **Overview** 

**Project's main features**

:point_right:  A website of a docker container hosted on Amazon ECS

:point_right: the container's image is from Amazon ECR

:point_right: the website use a Postgres DB from Amazon RDS to store the necessary infos

## **Architecture**

the diagram below illustrates the architecture(principle) of this project:

![](images/1-architecture.png)



## Continue Deployment

CloudFormation stack's deployment: see GitHub workflows https://github.com/lyc-handson-aws/handson-topic5/blob/main/.github/workflows/action-cf.yaml

Image service's deployment when a new image's version pushed : see Codebuild spec https://github.com/lyc-handson-aws/handson-topic4/blob/main/buildspec.yml

## **CloudFormation Stack Quick-create Link**

Click here to quickly create a same project with the same AWS resources:  [here](https://eu-west-3.console.aws.amazon.com/cloudformation/home?region=eu-west-3#/stacks/create/review?templateURL=https://s3bucket-handson-topic1.s3.eu-west-3.amazonaws.com/CF-template-handson-topic5.yaml)

**See Stack's description for complete actions to reproduce the same project**

> the default stack's region "Europe (Paris) eu-west-3"

## **AWS Resources**

Project's AWS resources:

:point_right: AWS::ECS::Cluster

- Cluster basic conifuration

- AWS::ECS::CapacityProvider - assoicate autoscalinggroup to ecs

:point_right: AWS::AutoScaling::AutoScalingGroup

-  AWS::EC2::LaunchTemplate - ec2 template configuration

:point_right: AWS::SecretsManager::Secret

- Store Postgre master password

:point_right: AWS::RDS::DBInstance

- Postgres infra's configuration
- AWS::RDS::OptionGroup - DB version's configuration

:point_right: AWS::ECS::TaskDefinition

- Define container service unit param:
- Define required/limit CPU/MEM
- Define used image, port mapping , env vars
- Define log configuration with CloudWatch

:point_right:AWS::ECS::Service

- Launch container service

- Define container service desired count

- Define container service's infra type: EC2

- Assign pubic ip to EC2 of container service

:point_right:AWS::IAM::Role

- one - AWS built-in policy "AmazonECSTaskExecutionRolePolicy" for taskdefinition to be able to retrieve image from ECR + permission to retrieve Posrgres pwd from Secretsmanager
- one - necessary permissions on Cloudwatch for Postgres' logs
- one - AWS built-in policy "AmazonEC2ContainerServiceforEC2Role" for a EC2 based ECS



