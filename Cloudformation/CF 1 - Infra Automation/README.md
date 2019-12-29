Provision PoC infra 

Bootstrap:

1. Configure aws cli

2. Run these commands below, and change *bucket-name* to the one you like:
```
export BUCKET=<bucket-name>

aws s3 mb s3://$BUCKET

aws s3 sync ./ s3://cloudadvisory/infra --exclude ".git/*" --delete

aws cloudformation create-stack --stack-name cloudapp1 --template-body file://master.yaml --parameters  file://cloudapp1.json --tags Key=Name,Value="CloudAdvisory"

aws cloudformation create-stack --stack-name cloudapp2 --template-body file://master.yaml --parameters  file://cloudapp2.json --tags Key=Name,Value="CloudAdvisory"

aws cloudformation delete-stack --stack-name infra

aws ec2 create-key-pair --key-name ca_ssh_key --query 'KeyMaterial' --output text > ca_ssh_key.pem

```

3. Store the `ca_ssh_key.pem` to parameter store and remove the local private key file:

```
aws ssm put-parameter --name ca_ssh_private_key --type SecureString --value $(cat ca_ssh_key.pem | base64 --wrap 0)

rm cms_ssh_key.pem
```

4. To share the private key with other iam users, ask them to run this command:
```
aws ssm get-parameter --name ca_ssh_private_key --with-decryption --query 'Parameter.Value' --output text | base64 -d > ca_ssh_key.pem
```
