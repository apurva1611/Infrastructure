# Infrastructure

How to set up infrastructure?
aws cloudformation --profile dev create-stack \
  --stack-name stack \
  --parameters file://vars.json\
  --template-body file://networking.json
