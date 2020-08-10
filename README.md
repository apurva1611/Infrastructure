### Infrastructure
Repsoitory to build infrastructure needed for bill tracking application. 
Implements Infrastructure as code using AWs-CLoudformation.

## How to set up infrastructure?
1. Download AWS CLI.
2. Create IAM user(devProfileAWS) in dev account with administrator access using AWS Console.
3. Using AWS ClI confgure the IAM user created above as a dev profile on your system:Dev Command is : aws configure --profile dev 
   After this command enter your secret key,access key and region of your IAM user. 
4. Create IAM user(ProdProfileAWS) in prod account with administrator access using AWS Console.
5. Using AWS ClI confgure the IAM user created above as a dev profile on your system:Dev Command is : aws configure --profile prod 
   After this command enter your secret key,access key and region of your IAM user.
6.  There are two files networking.json and autoScaling.json
7.  networking.json has code to setup all application and networking stack without load balancers and autoscaling.
8.  autoScaling.json has code of networking.json plus the code to enable load balancers,autoscaling,doamin configuration and       application and web security.
9. vars.json has all parameters needed in networking.json and autoscaling.json
10. To create infrastructure of networking.json use command:
    aws cloudformation --profile prod create-stack   --stack-name stack   --parameters file://vars.json  --template-body file://networking.json --capabilities CAPABILITY_IAM CAPABILITY_NAMED_IAM
    To create stack in dev profile just replace prod with dev.
11. Create stack by this command for autoScaling.json:aws cloudformation --profile prod create-stack \
  --stack-name stack \
  --parameters file://vars.json\
  --template-body file://autoScaling.json
Command :
 aws cloudformation --profile prod create-stack   --stack-name stack   --parameters file://vars.json  --template-body file://autoScaling.json --capabilities CAPABILITY_IAM CAPABILITY_NAMED_IAM
12. To generate SSH Keypair:
ssh-keygen -t rsa : enter filename where u want to generate key pair:
Put .pub file in Keypairs in ec2.And use the key pair name to generate ec2 in parameters in vars.json.
SSH into instance using following command:
in this the keypair is in .ssh folder with name aws-prod.
ssh -i ~/.ssh/aws-prod.pem ubuntu@54.147.45.160
ssh -i .ssh/awsProd ubuntu@(Public Ip4 addresss of instance lunched)
13. Get the AMI id by running ami repository ci and get ami ID

13. how to import certificate into aws:
aws --profile prod acm import-certificate --certificate file://Certificate.pem \
                                 --certificate-chain file://CertificateChain.pem \
                                 --private-key file://PrivateKey.pem


