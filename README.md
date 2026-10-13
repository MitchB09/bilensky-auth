# Bilensky Auth
Central User Management Pool for Bilensky Apps. 

Created to allow all personal apps to use a single, shared, userpool rather than having each service configure and manage thier own. Reduces duplication and overall cloud spend.


## Exports

| Export | Value | Description |
| --- | --- | --- |
| bilensky-auth-UserPoolId | `!Ref UserPool` | ID of the cognito user pool |
| bilensky-auth-UserPoolArn | `!GetAtt UserPool.Arn` | Full ARN of the cognito user pool |
| bilensky-auth-UserPoolDomain | `!Ref UserPoolDomain` | Public domain name for Authentication |

## Usage 

Exported values above can be leveraged in other SAM/CloudFormation stacks to reference the userpool ID, userpool ARN, or domain name in child projects.  

Here's an example for creating a UserPoolClient for a project:
```yaml
  UserPoolClient:
    Type: AWS::Cognito::UserPoolClient
    Properties:
      ClientName: 'my-app-user-pool-client'
      UserPoolId: !ImportValue "bilensky-auth-UserPoolId"

```

## Setup

To build the AWS SAM template first execute the following to compile template.yaml:

```bash
sam build
sam deploy --guided
```

Deploying Infra to dev environment

```bash
sam deploy --config-file samconfig.toml
```

Deploying to Prod

```bash
sam deploy --config-file samconfig.toml --config-env prod
```

## References
 - [AWS::Cognito:UserPool CloudFormation AWS Documentation](https://docs.aws.amazon.com/AWSCloudFormation/latest/TemplateReference/aws-resource-cognito-userpool.html)
 - [AWS::Cognito::UserPoolDomain CloudFormation AWS Documentation](https://docs.aws.amazon.com/AWSCloudFormation/latest/TemplateReference/aws-resource-cognito-userpooldomain.html#aws-resource-cognito-userpooldomain--examples--Creating_a_new_custom_domain_for_a_user_pool)
 - [!ImportValue Template Documentation](https://docs.aws.amazon.com/AWSCloudFormation/latest/TemplateReference/intrinsic-function-reference-importvalue.html)
