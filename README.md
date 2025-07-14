# AWS JSON Configurations

This repository contains a collection of AWS service configuration files in JSON format. These configurations provide templates and examples for setting up various AWS services and their integrations.

## 📁 File Overview

### 1. API Gateway OpenAPI Spec.json
**Purpose**: OpenAPI specification for Amazon API Gateway

This file contains an OpenAPI (Swagger) specification fragment that defines:
- API Gateway endpoint configuration for `/users` path
- GET method implementation
- Lambda proxy integration setup
- Response definitions

**Key Features**:
- AWS Lambda proxy integration
- Standard REST API endpoint definition
- HTTP 200 response configuration

**Use Case**: Use this as a template for creating API Gateway REST APIs with Lambda backend integration.

---

### 2. CloudFormation (S3 + Lambda + API Gateway).json
**Purpose**: CloudFormation template resources for serverless architecture

This file contains CloudFormation resource definitions for:
- IAM execution role for Lambda functions
- API Gateway method integration with Lambda
- Cross-service permissions and policies

**Key Components**:
- `LambdaExecutionRole`: IAM role with basic Lambda execution permissions
- `ApiMethod`: API Gateway integration configuration
- Lambda function ARN references and invoke permissions

**Use Case**: Deploy a complete serverless API stack with proper IAM permissions and service integrations.

---

### 3. IAM Policy (S3_DynamoDB).json
**Purpose**: IAM policy for DynamoDB operations

This policy grants permissions for:
- `dynamodb:PutItem` - Write data to DynamoDB table
- `dynamodb:GetItem` - Read single items from DynamoDB table
- `dynamodb:Query` - Query DynamoDB table with conditions

**Target Resource**: `arn:aws:dynamodb:*:*:table/AppTable`

**Use Case**: Attach this policy to IAM roles or users that need to interact with DynamoDB tables in your application.

---

### 4. Lambda Event (S3 Trigger).json
**Purpose**: S3 event structure for Lambda triggers

This file contains a sample S3 event payload that Lambda receives when triggered by S3 bucket events:
- Event version: 2.1
- Event type: Object creation (PUT operation)
- Source bucket: `upload-bucket`
- Object key: `incoming/file.csv`

**Use Case**: 
- Testing Lambda functions that process S3 events
- Understanding S3 event structure for development
- Integration testing with S3 triggers

---

### 5. Step Functions State Machine.json
**Purpose**: AWS Step Functions state definition

This file contains a state machine step configuration for:
- Running AWS Glue jobs
- Job parameter configuration
- Timeout settings (300 seconds)

**Key Features**:
- Glue job execution with configurable parameters
- Timeout protection for long-running data processing jobs
- Integration with AWS Glue for ETL operations

**Use Case**: Orchestrate data processing workflows using AWS Glue within Step Functions state machines.

---

## 🚀 Getting Started

### Prerequisites
- AWS CLI configured with appropriate credentials
- AWS account with necessary service permissions
- Basic understanding of AWS services (Lambda, API Gateway, S3, DynamoDB, Step Functions, Glue)

### Usage Instructions

1. **API Gateway Setup**:
   ```bash
   # Use the OpenAPI spec to create or update API Gateway
   aws apigateway put-rest-api --rest-api-id YOUR_API_ID --body file://API\ Gateway\ OpenAPI\ Spec.json
   ```

2. **CloudFormation Deployment**:
   ```bash
   # Deploy the CloudFormation stack
   aws cloudformation deploy --template-body file://CloudFormation\ \(S3\ +\ Lambda\ +\ API\ Gateway\).json --stack-name my-serverless-stack
   ```

3. **IAM Policy Application**:
   ```bash
   # Create or update IAM policy
   aws iam create-policy --policy-name DynamoDBAccess --policy-document file://IAM\ Policy\ \(S3_DynamoDB\).json
   ```

4. **Lambda Testing with S3 Events**:
   ```bash
   # Test Lambda function with S3 event payload
   aws lambda invoke --function-name YOUR_FUNCTION --payload file://Lambda\ Event\ \(S3\ Trigger\).json response.json
   ```

5. **Step Functions State Machine**:
   ```bash
   # Create or update Step Functions state machine
   aws stepfunctions create-state-machine --name MyStateMachine --definition file://Step\ Functions\ State\ Machine.json --role-arn YOUR_ROLE_ARN
   ```

## 🏗️ Architecture Overview

These configurations work together to create a comprehensive serverless data processing pipeline:

```
S3 Bucket → Lambda Function → DynamoDB
    ↓
API Gateway → Lambda Function → DynamoDB
    ↓
Step Functions → Glue Job → Data Processing
```

## 📝 Configuration Notes

- **Region-specific**: Update ARNs and region-specific values before deployment
- **Resource Names**: Customize resource names (table names, bucket names, etc.) for your environment
- **Permissions**: Ensure proper IAM permissions are in place before deploying
- **Dependencies**: Some configurations depend on existing AWS resources

## 🔧 Customization

Before using these configurations:

1. Replace placeholder values (e.g., `YOUR_API_ID`, `AppTable`, `upload-bucket`)
2. Update ARNs to match your AWS account and region
3. Modify timeout values and other parameters as needed
4. Add additional IAM permissions if required for your use case

## 📚 Additional Resources

- [AWS CloudFormation Documentation](https://docs.aws.amazon.com/cloudformation/)
- [API Gateway OpenAPI Extensions](https://docs.aws.amazon.com/apigateway/latest/developerguide/api-gateway-swagger-extensions.html)
- [Lambda Event Sources](https://docs.aws.amazon.com/lambda/latest/dg/lambda-services.html)
- [Step Functions State Language](https://docs.aws.amazon.com/step-functions/latest/dg/concepts-amazon-states-language.html)
- [DynamoDB IAM Policies](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/security-iam.html)

## 🤝 Contributing

Feel free to submit issues and enhancement requests. When contributing:
1. Follow AWS best practices
2. Include proper documentation
3. Test configurations before submitting
4. Update this README when adding new configurations

## 📄 License

This project is provided as-is for educational and development purposes. Please review AWS pricing and service limits before deploying to production environments.

---

**Last Updated**: July 14, 2025
**Repository**: AWS-JSON-Configurations
**Owner**: oyebiyisunday
