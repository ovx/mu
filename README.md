<img src="https://github.com/stelligent/mu/wiki/img/mu.png" width="150">
<br/>

[![Build Status](https://circleci.com/gh/stelligent/mu.svg?style=shield)](https://circleci.com/gh/stelligent/mu) [![Join the chat at https://gitter.im/stelligent/mu](https://badges.gitter.im/stelligent/mu.svg)](https://gitter.im/stelligent/mu?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge) [![Go Report Card](https://goreportcard.com/badge/github.com/stelligent/mu)](https://goreportcard.com/report/github.com/stelligent/mu)


# Why?
Both Amazon ECS (Elastic Container Service) and Amazon EKS (Elastic Container Service for Kubernetes) provide excellent platforms for deploying microservices as containers.  The challenge however is that there is a significant learning curve for microservice developers to deploy their applications in an efficient manner.  Specifically, they must learn to use CloudFormation to orchestrate the management of EKS, ECS, ECR, EC2, ELB, VPC, and IAM resources.  Additionally, tools like CodeBuild and CodePipeline must be mastered to create a continuous delivery pipeline for their microservices.

To address these challenges, this tool was created to simplify the declaration and administration of the AWS resources necessary to support microservices.  Similar to how the [Serverless Framework](https://serverless.com/) improved the developer experience of Lambda and API Gateway, this tool makes it easier for developers to use EKS or ECS as a microservices platform.

The `mu` tool uses CloudFormation stacks to manage all resources it creates.  Additionally, `mu` will not create any databases or other AWS resources to support itself.  It will only create resources (via CloudFormation) necessary to run your microservices.  This means at any point you can stop using `mu` and continue to manage the AWS resources that it created via AWS tools such as the CLI or the console.

![Architecture Diagram](https://github.com/stelligent/mu/wiki/img/mu-architecture.gif)

# Demo
Watch the 90 second demo below to see mu in action!

![Demo](https://github.com/stelligent/mu/wiki/quickstart/mu-quickstart.gif)

# Get Started!
Install latest version to /usr/local/bin (or for additional options, see [wiki](https://github.com/stelligent/mu/wiki/Installation)):

```bash
curl -s https://getmu.io/install.sh | sudo sh
```
Verify installation
```bash
mu -v
mu version 1.5.10
```

Assuming your project already has a Dockerfile, you can initialize your mu.yml file with: `mu init`.  More details available in the [quickstart](https://github.com/stelligent/mu/wiki/Quickstart).

# What's next?
Check out the [examples](examples) to see snippets of `mu.yml` configuration files that you can use in your own project:

* **[Basic](examples/basic)** - Simple website with continuous delivery pipeline deploying to dev and prod environments
* **[EKS](examples/eks)** - Demonstration of using EKS provider for mu
* **[Test Automation](examples/pipeline-newman)** - Automating end-to-end testing via [Newman](https://github.com/postmanlabs/newman)
* **[RDS Database](examples/database)** - Defining a database for a service
* **[Env Variables](examples/service-env-vars)** - Defining environment variables for the service
* **[HTTPS](examples/elb-https)** - Enable HTTPS on the ALB for an environment
* **[DNS](examples/elb-dns)** - Associate Route53 resource record with ALB for an environment
* **[VPC Target](examples/vpc-target)** - Targeting an existing VPC for an environment
* **[VPN Connection](examples/vpn)** - Demonstration of adding VPN via CloudFormation
* **[Custom CloudFormation](examples/custom-cloudformation)** - Demonstration of adding custom AWS resources via CloudFormation
* **[Traditional Infrastructure](examples/ec2-provider)** - Demonstration of using EC2 + CodeDeploy rather than ECS for running services

Refer to the wiki for complete details on the configuration of `mu.yml` and the cli usage:

* **[Environments](https://github.com/stelligent/mu/wiki/Environments)** - managing VPCs, ECS clusters, container instances and ALBs
* **[Services](https://github.com/stelligent/mu/wiki/Services)** - managing ECS service configuration
* **[Databases](https://github.com/stelligent/mu/wiki/Databases)** - managing database configuration
* **[Pipelines](https://github.com/stelligent/mu/wiki/Pipelines)** - managing continuous delivery pipelines
* **[IAM](https://github.com/stelligent/mu/wiki/IAM)** - managing IAM roles that mu uses
* **[EKS](https://github.com/stelligent/mu/wiki/EKS)** - using EKS instead of ECS for environment provider
* **[CLI](https://github.com/stelligent/mu/wiki/CLI-Usage)** - details about using the CLI
* **[Custom CloudFormation](https://github.com/stelligent/mu/wiki/Custom-CloudFormation)** - details about customizing the CloudFormation that is generated by mu.
* **[Service Discovery](https://github.com/stelligent/mu/wiki/Service-Discovery)** - details about configuring and using service discovery
* **[Traditional Infrastructure](https://github.com/stelligent/mu/wiki/Traditional-Infrastructure)** - details about using traditional infrastructure (EC2 instances) for running services, rather than ECS and Docker.

# Support

Need help?  Check out the [FAQ](https://github.com/stelligent/mu/wiki/FAQ) to try to find an answer to your question.  If you can't find an answer there, ask on [Gitter](https://gitter.im/stelligent/mu)!

# Contributing

Want to contribute to Mu?  Awesome!  Check out the [contributing guidelines](CONTRIBUTING.md) to get involved.

## Building from source

* Ensure [AWS CLI](http://docs.aws.amazon.com/cli/latest/userguide/cli-chap-getting-started.html) is configured with an access key, secret access key, and region.
* Install Go tools 1.10+ - (https://golang.org/doc/install)
* Clone this repo `git clone git@github.com:stelligent/mu.git $GOPATH/src/github.com/stelligent/mu`
* Go to src `cd $GOPATH/src/github.com/stelligent/mu`
* Build with `make`
* Run unit tests with `make test`
* Run end-to-end tests with `make e2e`...takes about 30 minutes and will incur charges in your AWS account.
