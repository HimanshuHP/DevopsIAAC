## Deploy a High-Availability Web App using CloudFormation

# PROJECT SPECIFICATION:

## Project Introduction

Your company is creating an Instagram clone called Udagram. Developers pushed the latest version of their code in a zip file located in a public S3 Bucket.

You have been tasked with deploying the application, along with the necessary supporting software into its matching infrastructure.

This needs to be done in an automated fashion so that the infrastructure can be discarded as soon as the testing team finishes their tests and gathers their results.

There will be two parts to this project:

You'll first develop a diagram that you can present as part of your portfolio and as a visual aid to understand the CloudFormation script.
The second part is to interpret the instructions as well as your own diagram and create a matching CloudFormation script.

## Project Requirements

### Server spec

You'll need to create a Launch Configuration for your application servers in order to deploy four servers, two located in each of your private subnets. The launch configuration will be used by an auto-scaling group.

You'll need 2 vCPUs and at least 4GB of RAM. The Operating System to be used is Ubuntu 18. So, choose an Instance size and Machine Image (AMI) that best fits this spec. Be sure to allocate at least 10GB of disk space so that you don't run into issues.

### Security Groups and Roles

Since you will be downloading the application archive from an S3 Bucket, you'll need to create an IAM Role that allows your instances to use the S3 Service.

Udagram communicates on the default HTTP Port: 80, so your servers will need this inbound port open since you will use it with the Load Balancer and the Load Balancer Health Check. As for outbound, the servers will need unrestricted internet access to be able to download and update its software.

The load balancer should allow all public traffic (0.0.0.0/0) on port 80 inbound, which is the default HTTP port. Outbound, it will only be using port 80 to reach the internal servers.

The application needs to be deployed into private subnets with a Load Balancer located in a public subnet.

One of the output exports of the CloudFormation script should be the public URL of the LoadBalancer.

Bonus points if you add http:// in front of the load balancer DNS Name in the output, for convenience.

# SOLUTION:

### Architecture Diagram

![Diagram](udagram_architecture.png)


#### Usage

> Install [AWS CLI](https://aws.amazon.com/cli/) installed.

```
aws --version
```

> Usage:

```
./create.sh (stackName) (script.yml) (parameters.json)
```

> Example:

```
./create.sh udagram-iaac-servers servers.yml servers.json
```

1. Create cloud formation stack using `infra.yml` and `infra.json` to create VPC, Internet Gateway, Subnets in availability zone.
2. Next , Create cloud formation stack using `servers.yml` and `servers.json` to setup ec2 instances, load balancer and autoscaling group

# Website Link :

[http://udagr-webap-1v6u8ylwo9j1w-1515667053.us-west-2.elb.amazonaws.com](http://udagr-webap-1v6u8ylwo9j1w-1515667053.us-west-2.elb.amazonaws.com)
