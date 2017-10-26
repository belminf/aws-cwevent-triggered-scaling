# aws-cwevent-triggered-scaling

Trigger auto-scaling via a CloudWatch Events.

Went down this route because [ASG Scheduled Actions](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-as-scheduledaction.html) only support a simplified version of cron (e.g., `0 19 * * *`) instead of more flexible cron format that CloudWatch Events support (e.g., every 4th Thursday of the month would be `0 3 ? * 4#4 *`).

## Example run

    aws cloudformation create-stack --capabilities CAPABILITY_IAM --template-body file://template.yaml --stack-name foobar --parameters ParameterKey=KeyName,ParameterValue=belminf@gmail.com-20171025 ParameterKey=AMI,ParameterValue=ami-8c1be5f6
