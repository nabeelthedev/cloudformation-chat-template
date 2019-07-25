## Description

A CloudFormation template for chat/messaging resources.

This template configures a chat stack with the following features.

### GraphQL via AppSync

The chat functionality is built using resolvers through AppSync, a managed GraphQL service. The resolvers are written in Velocity Template Language (VTL) and perform various data validations like verifying users have permission to post messages to a group. The resolvers also perform read and writes through DynamoDB and Lambda.

### How the system works

A user creates a group and gives it a name. The system will provide an invite link when the user wants to invite people to a group. Users who want to join a group will use the invite link. Users can post messages in a group and will recieve real-time updates when new messages are posted.

## Requirements

1. S3 bucket to upload Lambda functions.

## Install

1. `aws cloudformation package --s3-bucket your-bucket --template-file ./template.yaml --output-template-file packaged-template.yaml`
2. `aws cloudformation create-stack --stack-name stack-name --template-body file://packaged-template.yaml --capabilities CAPABILITY_NAMED_IAM --parameters ParameterKey=UserPoolId,ParameterValue=auth-stack-UserPoolId`

Fill in parameters above with your information (i.e. _your-bucket_, _stack-name_). _UserPoolId_ is the exported User Pool Id from _cloudformation-auth-template_.
