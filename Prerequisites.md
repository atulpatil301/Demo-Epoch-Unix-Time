## Table of Contents

*   [Prerequisites](#prerequisites)
*   [When you use AWS CloudFormation](#When-you-use-AWS-CloudFormation)
*   [How Does AWS CloudFormation Work?](#How-Does-AWS-CloudFormation-Work?)
*   [AWS CloudFormation Service Role](#AWS-CloudFormation-Service-Role)
*   [Custom Resource Helper](#Custom-Resource-Helper)
*   [CloudFormation Template Anatomy](#CloudFormation-Template-Anatomy)
*   [Running the templates](#Running-the-templates)
*   [Issues?](#Issues?)


## Prerequisites

To this assignment you will need the following tools/setup/knowledge:

*   AWS Account
*   Laptop
*   Secure shell (ssh) to login CLI
    *   Mac OS/Linux: command lines tools are installed by default
    *   Windows
        *   Putty: ssh client: [http://www.putty.org/](http://www.putty.org/)
    *   Access key and secret key or console access
    *   Access Key and Secret key genrated form IAM Users.
    *   Configure AWS CLI or access using console from credentials.
    *   User should have access of create IAM role for this task only.
    *   Should have access to create, update and delete cloudformation template.
    
## When you use AWS CloudFormation

You create templates to describe your AWS resources and their properties. Whenever you create a stack, AWS CloudFormation provisions the resources that are described in your template. 

## How Does AWS CloudFormation Work?

When you create a stack, AWS CloudFormation makes underlying service calls to AWS to provision and configure your resources. Note that AWS CloudFormation can perform only actions that you have permission to do. For example, to create EC2 instances by using AWS CloudFormation, you need permissions to create instances. You'll need similar permissions to terminate instances when you delete stacks with instances

## AWS CloudFormation Service Role

A service role is an AWS Identity and Access Management (IAM) role that allows AWS CloudFormation to make calls to resources in a stack on your behalf. You can specify an IAM role that allows AWS CloudFormation to create, update, or delete your stack resources. By default, AWS CloudFormation uses a temporary session that it generates from your user credentials for stack operations. If you specify a service role, AWS CloudFormation uses the role's credentials.

Use a service role to explicitly specify the actions that AWS CloudFormation can perform which might not always be the same actions that you or other users can do. For example, you might have administrative privileges, but you can limit AWS CloudFormation access to only Amazon EC2 actions. 
 
## Custom Resource Helper

The crhelper python script can be saved into your lambda zip to simplify best practice Custom Resource creation. It provides exception and timeout trapping, sending responses to CloudFormation and provides detailed, configurable logging.

In order to use it in your custom resource function, save crhelper.py in the root of your function zip path. Your handler file will then only need to import crhelper, define any init code and functions for create,update and delete events.

## CloudFormation Template Anatomy

```
---
AWSTemplateFormatVersion: "version date"

Description:
  String

Metadata:
  template metadata

Parameters:
  set of parameters

Mappings:
  set of mappings

Conditions:
  set of conditions

Transform:
  set of transforms

Resources:
  set of resources

Outputs:
  set of outputs
```

## Running the templates

Note: these directions assume you have the AWS CLI installed and configured. Using below mention commands we can deploy, update and delete stack.

```
STACK_NAME  := epoch
TEMPLATE    := epoch.yaml
PARAM_STATE := London

all:

deploy-stack:
	aws cloudformation deploy \
		--template-file $(TEMPLATE) \
		--stack-name $(STACK_NAME) \
		--parameter-overrides State=$(PARAM_STATE) \
		--capabilities CAPABILITY_IAM

update-stack:
	aws cloudformation update-stack \
		--stack-name $(STACK_NAME) \
		--template-body file://./$(TEMPLATE) \
		--parameters ParameterKey=State,ParameterValue=$(PARAM_STATE) \
		--capabilities CAPABILITY_IAM

delete-stack:
	aws cloudformation delete-stack --stack-name $(STACK_NAME)
```
   
 
 ## Issues?
 
When i am working on this task, I got falled couple of time because of not having proper access, like IAM role, cloudformation full access & i fix it access issue.

I search custome resource & found cfnresponce and request modules for python. Which saved my time. :)
