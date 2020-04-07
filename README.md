# Infrastructure

How to set up infrastructure?
1. Download AWS CLI.
2. Create IAM user(devProfileAWS) in dev account with administrator access using AWS Console.
3. Using AWS ClI confgure the IAM user created above as a dev profile on your system:Dev Command is : aws configure --profile dev - credentails of user devProfileAWS. 
4. Create stack by this command:aws cloudformation --profile pord create-stack \
  --stack-name stack \
  --parameters file://vars.json\
  --template-body file://autoScaling.json

 aws cloudformation --profile prod create-stack   --stack-name stack   --parameters file://vars.json  --template-body file://autoScaling.json --capabilities CAPABILITY_IAM CAPABILITY_NAMED_IAM



