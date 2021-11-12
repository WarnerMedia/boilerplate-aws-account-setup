# Boilerplate for AWS Account Setup

## Overview

The purpose of this repository is to help you set up a solid base infrastructure in a given AWS region using Infrastructure-as-Code (IaC).

This repository uses CloudFormation and AWS CodePipeline to create and maintain the infrastructure.  However, you are not bound to CloudFormation for projects that you use with this infrastructure.  All key values are output as either SSM Parameters or Secrets Manager secrets.  So if your IaC solution can read values from SSM Parameters and Secrets Manager, you should be all set.

## What is Included?

This is a short list of some of the things you get if you use this full solution:

1. Individual KMS keys for core services.
2. Some essential S3 buckets with proper encryption.
3. CodeBuild GitHub credential configuration (optional)
4. Creation of a Route53 hosted zone for your domain (optional)
5. Creation of DNS-verified secure certificates for the above hosted zone (optional)
6. Some general service roles.
7. Fully-configured VPC with public and private subnets, NATs, EIPs, IPv6, three availability zones, and more.
8. A bastion instance which can be used to reach instances in your VPC.
9. A large number of SSM parameters with values for things in the infrastructure (such as the VPC ID).
10. Some secrets in Secrets Manager which hold things like the GitHub token.

## Quick Start

1. Create your own copy of this repository in GitHub.
2. From a local checkout of your new repository, locate the `v1/iac/cfn/setup/main.yaml` file.
3. Log into your AWS account.
4. Select your region.
5. Go to the CloudFormation console.
6. Use the `v1/iac/cfn/setup/main.yaml` file to create a stack.
7. Fill in answers to all of the template parameters.
8. Run the stack.
9. The stack will create the CodePipelines needed to get things running.
10. If all of the parameter values were valid, it should take about 20 to 30 minutes to set up the infrastructure in this region.

## Detailed Start

1. This repository is meant to be used as a starting template, so please make use of the "Use this template" button in the GitHub console to create your own copy of this repository.
2. Make a local clone of the new repository that you just created.
3. You are going to need a [GitHub Personal Access Token](https://docs.github.com/en/github/authenticating-to-github/creating-a-personal-access-token) from a service account (which has full private repository access to your new private repository).  It it not recommended that you use a Personal Access Token from your personal GitHub user for security reasons, but one could be used in the short-term to get things up-and-running.
4. Make sure the user with the Private Access Token has full admin. access to the repository (this will be needed temporarily to initially create the WebHook).
5. Log into your AWS account via the console.
6. Select the region where you want to set up the infrastructure.
7. Go to the CloudFormation console in that region.
8. Select the "Create stack" dropdown.
9. Select "With new resources (standard)" from the dropdown.
10. Select "Template is ready".
11. Select "Upload a template file".
12. Upload the following file from your local checkout of the repository: `v1/iac/cfn/setup/main.yaml`
13. Click "Next"
14. You will be presented with a form that has a lot of fields, these fields each have a description which attempts to explain what you need to fill in for that given field.  The hope is that most of these are self-explanatory to anyone well-versed in AWS technologies.
15. Please note that the first form field is just a suggested name for the stack, you can name the stack whatever you would like, but if you name it with the suggested stack name, it might make it easier to find in the future.
16. Keep clicking on the "Next" button until you see a screen where you can review your parameters.
17. Once you have reviewed these parameters, you can click on the "Create stack" button, and CloudFormation will start setting up your infrastructure.  If all goes smoothly, this will take about 20 to 30 minutes for CloudFormation to set everything up.

## Individual/Modular Service Templates

Though this infrastructure is intended to all be created and maintained via the CodePipeline solution, it should be noted that the templates have generally been divided up per service.

If you don't want to use the full solution, you could, for instance, take the `v1/iac/cfn/vpc/main.yaml` template as a starting point and modify it for your purposes (just to get the VPC up).  However, the VPC template will not work individually without some modifications as it will expect some base-level SSM parameters to exist.

If you want to modify how CloudFormation is creating something, you should be able to easily find the specific template by looking in the `v1/iac/cfn/` folder.

## Template Parameter/Environment Files

In the `env/cfn` folder, you will find a number of JSON files.  These files can be used to pass template configuration values to the individual templates.  There is documentation here: https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/continuous-delivery-codepipeline-cfn-artifacts.html#w2ab1c13c17c15

## Active Project Community Leader(s)

Every open source project has an individual or individuals who are community leaders of the project.

The following is a list of community leaders that can be contacted for questions around contributions, documentation, issues, etc.

### WarnerMedia

* [Neal Gamradt](mailto:neal.gamradt@warnermedia.com)
* [Ian Turner](mailto:ian.m.turner@warnermedia.com)

## Contributing to the Project

### WarnerMedia Employees

Contributions from WarnerMedia employees must follow an internal corporate contribution process in order to protect corporate intellectual property.

WarnerMedia employees cannot contribute via the process outlined for external contributors.

Please contact one of the active project community leaders (who is an employee of WarnerMedia) to get details on the process for internal contributions.

### External Contributors

If you are not a WarnerMedia employee, please follow the instructions listed in the [How to Contribute](CONTRIBUTING.md) document.

## TODO List

### Required

1. Improve overall documentation.
2. Add a testing CodeBuild instance for testing the infrastructure using Cucumber tests.
3. Audit SSM parameters to double-check names and values.

### Optional

1. Interactive setup shell script which would allow for deployment to multiple accounts and regions.
2. Testing the CLA with a PR from an internal account.  I should not get the CLA notice.
