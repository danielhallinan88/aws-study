# aws-study
## Create and SNS Topic with an SQS Queue subscription
```
aws cloudformation create-stack --stack-name sns-sqs-chain --template-body file://sns-sqs-template.yaml
```
## Create and SNS Topic with an SQS Queue subscription and a Lambda consumer
```
aws cloudformation create-stack --stack-name sns-sqs-lambda-chain --template-body file://sns-sqs-python-lambda-template.yaml --capabilities CAPABILITY_NAMED_IAM
```
