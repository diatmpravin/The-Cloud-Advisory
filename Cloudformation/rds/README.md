### Provision PoC infra 

```
aws cloudformation create-stack --stack-name rds --template-body file://rds.yaml --parameters ParameterKey=SubnetId1,ParameterValue=subnet-019844b586b3a73ed ParameterKey=VpcId,ParameterValue=vpc-0abd3e892b3173fef ParameterKey=DBPassword,ParameterValue=Test1234 ParameterKey=DBUser,ParameterValue=dbroot --tags Key=Name,Value="rds"

aws cloudformation delete-stack --stack-name rds
```