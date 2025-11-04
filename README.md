### Create Stack
 aws cloudformation create-stack --template-body file://vm_cf_template.yaml --stack-name EC2DemoStack

### Update Stack 
ws cloudformation update-stack  --template-body file://vm_cf_cloudwatch.yaml --stack-name EC2DemoStack

### Deploy Stack

aws cloudformation deploy \
  --stack-name EC2DemoStack \
  --template-file vm_cf_template.yaml \
  --parameter-overrides \
      KeyName=MyDemoKey \
      VpcId=vpc-0c7fb146d4f8ef317 \
      SubnetId=subnet-0a1c23d34e5f69h7g \
  --capabilities CAPABILITY_NAMED_IAM


### Delete Stack / CLEAN UP 
aws cloudformation delete-stack --stack-name EC2DemoStack
aws cloudformation wait stack-delete-complete --stack-name EC2DemoStack

### then deploy again with updated parameters containing cloudwatch
  --stack-name EC2DemoStack \
  --template-file vm_cf_cloudwatch.yaml \
  --parameter-overrides KeyName=MyDemoKey \
  --capabilities CAPABILITY_NAMED_IAM


### List subnets 
aws ec2 describe-subnets \
  --query "Subnets[*].{SubnetId:SubnetId,VpcId:VpcId,AZ:AvailabilityZone,Public:MapPublicIpOnLaunch}" \
  --output table