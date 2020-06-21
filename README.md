# API Gateway Challenge

## Application
This cloudformation will create the following main resources:
- Dynamo DB table with dynamo DB streams enabled
- Lambda function to process POST API requests and enter data to table
- API gateway for above lambda with API key authentication
- Lambda function to process table insert streams and send SNS notification email

Application expects POST requests with API key in the following JSON format:
>{ 
>
>	"team_name": "Pacers", 
>
>	"team_country": "USA", 
>
>	"team_desc": "NBA team",
>
>	"team_rating": "5"
>
>}

API gateway uses the API key to authenticate request and forwards to lambda function which enters the data to dynamo DB table. Dynamo DB streams are generated which are processed by second lambda function which sends message to SNS topic, which is subscribed to email notification. 

## Prerequisites
The following packages should be available in your system:
- aws-cli
- Python

## Deploy application
- Ensure you have configured AWS profile correctly using `aws configure` command
- Set AWS_PROFILE env var
- Run `aws cloudformation deploy --template-file cloudformation.yaml --stack-name <stackName> --capabilities CAPABILITY_IAM --parameter-overrides PushEmail=<example@email.com>`. Replace <stackName> and <example@email.com> with appropriate values for the name of cloudformation stack and the email to where you wish to recieve sns push notifications.
- Run `aws cloudformation describe-stacks --stack-name <stackName>` to get the outputs for the stack
- Make a note of `RootUrl` and `ApiKey`
- Run `aws apigateway get-api-key --api-key <ApiKey> --include-value`. Replace <ApiKey> with value from previous step
- Make note of ApiKey `value` in the output

## Test application
- Create POST request to `<RootUrl>v1/add_new`. Replace <RootUrl> with value from deployment outputs
- Add `x-api-key` header with value from deployment outputs
- Add body as described above, changing the field values as needed for each table entry
- Send request
- On first run of application, you'll recieve email to verify your email address
- Now, for every new entry added to table, you'll recieve email notification

## Improvements:
- Add validation in lambda for POST body
- Dockerize application and add 3 musketeers for consistency between various run environments
- Add authentication using basic or cognito pools etc., rather than just API key
- Simplify process of getting stack output URL and API key, to get these displayed with just single deployment Make command
- Use serverless framework or terraform rather than cloudformation
