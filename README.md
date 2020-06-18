# API Gateway Challenge

## Background
A cloud engineer working for Company X created a Cloudformation template to deploy a serverless API
service which will receive and store data about sports teams into a NoSQL database.

After deploying the stack, although the AWS Cloudformation stack is successfully created, when the API
receives a POST request the engineer is facing some issues and data is not being written to the table as
expected.

The Cloudformation stack mainly deploys the following AWS resources:

|Service        |Description|
|---------------|-----------|
|API Gateway    |Handles the http traffic|
|Role           |Role to be used by Lambda Function|
|Lambda Function|Extract data from the http request and update the database|
|DynamoDB Table |NoSQL Database|

## Tasks
Based on this scenario, please work on below tasks:

**Main Task**

- Make the necessary changes so data is successfully written to the DynamoDB Table once a
POST request is received by the API Gateway.

**Secondary Task**

Pick one of following:
- Add any required resources to send a message to a SNS Topic whenever a new item is added to
the DynamoDB Table.
    - The message can be either table updated or the content of the new item added.
    
OR

- Implement any type of authentication to the API Gateway.

## Deliverables:
- Share your code with us through your own git repository. Remember to make your repository
private so only we can review it.
- Consider security on all pieces of your work.
- Make sure that all resources required by your stack are included on the deployment process.
- Include a README with details on how to run your code. Add a section with recommended
improvements for this stack.
- On the same README file, include a section with recommended improvements to be done on
the stack/repo that you consider important.
