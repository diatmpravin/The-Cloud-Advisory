### Provision PoC infra 

```
aws cloudformation create-stack --stack-name basic-web-server --template-body file://basic-amazon-ec2-instance.yaml --parameters ParameterKey=InstanceType,ParameterValue=t2.micro ParameterKey=KeyName,ParameterValue=ca ParameterKey=SubnetId1,ParameterValue=subnet-019844b586b3a73ed ParameterKey=VpcId,ParameterValue=vpc-0abd3e892b3173fef --tags Key=Name,Value="WebServer"

aws cloudformation delete-stack --stack-name basic-web-server

aws cloudformation create-stack --stack-name basic-rehl-ec2-instance1 --template-body file://basic-rehl-ec2-instance.yaml --parameters ParameterKey=InstanceType,ParameterValue=t2.micro ParameterKey=KeyName,ParameterValue=ca ParameterKey=SubnetId1,ParameterValue=subnet-019844b586b3a73ed ParameterKey=VpcId,ParameterValue=vpc-0abd3e892b3173fef --tags Key=Name,Value="WebServer"

aws cloudformation delete-stack --stack-name basic-rehl-ec2-instance1

```
#### EC2 instance with ELB

```
aws cloudformation create-stack --stack-name appserver-1 --capabilities CAPABILITY_IAM --template-body file://ec2-instances-with-application-load-balancer.yaml --parameters ParameterKey=Application,ParameterValue=cloudapp1 ParameterKey=KeyName,ParameterValue=Lab-2 --tags Key=Name,Value="cloudapp1"
```

#### EC2 instance with ELB, ASG

```
aws cloudformation create-stack --stack-name appserver-1 --capabilities CAPABILITY_IAM --template-body file://ec2-instances-with-application-elb-asg.yaml --parameters ParameterKey=Application,ParameterValue=cloudapp1 ParameterKey=KeyName,ParameterValue=Lab-2 --tags Key=Name,Value="cloudapp1"
```

#### EC2 instance with ELB, ASG, Scale-in/Scale-out Policy

```
aws cloudformation create-stack --stack-name appserver-1 --capabilities CAPABILITY_IAM --template-body file://ec2-instances-with-application-elb-asg-scaling-policy.yaml --parameters ParameterKey=Application,ParameterValue=cloudapp1 ParameterKey=KeyName,ParameterValue=Lab-2 --tags Key=Name,Value="cloudapp1"

ab -k -n 10000000000 -c 200 http://cloudapp1-dev-alb-280308358.eu-central-1.elb.amazonaws.com/
```