### Provision PoC infra 

```
aws cloudformation create-stack --stack-name rds-mysql --template-body file://rds.yaml --parameters ParameterKey=Application,ParameterValue=cloudapp1 ParameterKey=DBPassword,ParameterValue=cloudapp1  ParameterKey=AppServerSG,ParameterValue=sg-06fa066b25ec63892 --tags Key=Name,Value="cloudapp1"

aws cloudformation delete-stack --stack-name rds
```