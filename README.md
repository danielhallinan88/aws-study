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
This can be done with or without a VPC, but preferably done with a VPC.
1. Create a Security Group for the NAT instance. The Inbound rule consisting of port 443 from the subnet any private instances will be in, and add port 22 if you would like to SSH into the NAT instance, though this would be a security risk. For the Outbound Rule allow HTTPS traffice to 0.0.0.0/0.
2. Create NAT instance
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
3. Create a Security Group for private instances, with an inbound rule allowing SSH from a Bastion host. The Bastion host could also be the NAT instance.
4. Create a key pair for the private instances.
```
aws ec2 create-key-pair \
    --key-name MyNewKeyPair \
    --query 'KeyMaterial' \
    --output text > MyNewKeyPair.pem
```
5. Make the key read only.
```
chmod 400 MyNewKeyPair.pem
```
6. Create a private instance
```
aws ec2 run-instances \
    --image-id ami-037774efca2da0726 \
    --instance-type t2.micro \
    --key-name MyNewKeyPair \
    --subnet-id <YourSubnetId> \
    --security-group-ids <YourSecurityGroupId> \
    --no-associate-public-ip-address
```
