# aws-study
## Create and SNS Topic with an SQS Queue subscription
```
aws cloudformation create-stack --stack-name sns-sqs-chain --template-body file://sns-sqs-template.yaml
```
## Create and SNS Topic with an SQS Queue subscription and a Lambda consumer
```
aws cloudformation create-stack --stack-name sns-sqs-lambda-chain --template-body file://sns-sqs-python-lambda-template.yaml --capabilities CAPABILITY_NAMED_IAM
```
## Create an EC2 NAT Instance
```
aws ec2 run-instances \
    --image-id ami-037774efca2da0726 \
    --instance-type t2.micro \
    --subnet-id <YourSubnetId> \
    --security-group-ids <YourSecurityGroupId> \
    --associate-public-ip-address \
    --user-data file://ec2-nat-instance-user-data.txt \
    --tag-specifications 'ResourceType=instance,Tags=[{Key=Name,Value=NAT-Instance}]'
```
