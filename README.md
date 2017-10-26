# aws-cwevent-triggered-scaling

Trigger auto-scaling via a CloudWatch Events.

Went down this route because [ASG Scheduled Actions](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-as-scheduledaction.html) only support a simplified version of cron (e.g., `0 19 * * *`) instead of more flexible cron format that CloudWatch Events support (e.g., every 4th Thursday of the month would be `0 3 ? * 4#4 *`).

## Example run

Scales up to 2 at 3AM on the 2nd Sunday of the month and then scales down to 1 30 minutes later:

    aws cloudformation update-stack --capabilities CAPABILITY_IAM --template-body file://template.yaml --stack-name foobar --parameters ParameterKey=KeyName,ParameterValue=belminf@amazon.com ParameterKey=AMI,ParameterValue=ami-8c1be5f6 ParameterKey=ScaleUpCron,ParameterValue="0 3 ? * 1#2 *" ParameterKey=ScaleBackCron,ParameterValue="30 3 ? * 1#2 *"


## To-do
* Limit Lambda policy to only act on the actual ASG created
