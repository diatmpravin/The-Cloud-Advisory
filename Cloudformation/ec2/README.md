### Provision PoC infra 

```
aws cloudformation create-stack --stack-name basic-web-server --template-body file://basic-amazon-ec2-instance.yaml --parameters ParameterKey=InstanceType,ParameterValue=t2.micro ParameterKey=KeyName,ParameterValue=ca ParameterKey=SubnetId1,ParameterValue=subnet-019844b586b3a73ed ParameterKey=VpcId,ParameterValue=vpc-0abd3e892b3173fef --tags Key=Name,Value="WebServer"

aws cloudformation delete-stack --stack-name basic-web-server
```