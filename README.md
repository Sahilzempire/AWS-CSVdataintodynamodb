AWS Data Engineering projects.
Welcome to Project 1 in AWS Data engineering projects series.

This is basic level project that aims to "**To import CSV data into DynamoDB using Lambda and S3 Event Triggers**"

This is a readme file that is going to provide you summary about the Project. I have attached a PDF file that involves all the details about the services being used and also the steps used to achieve our goal.

As part of my learning curve on DynamoDB and its interaction with various AWS services, Here S3 event triggers an action on a Lambda function to import CSV data from S3 Bucket and do some transformation and saved into a DynamoDB table using AWS Management Console.

**Objectives:**
• Create an S3 bucket.
• Upload a CSV file.
• Creating Lambda Function with a timeout of more than 1 minute, 
which contains the code to import the CSV data into DynamoDB.
• Create a Amazon DynamoDB table.
• All associated IAM roles needed for the solution, configured 
according to the principle of least privilege.
• Test the CSV Data Import in Lambda
• Adding Event Triggers to the S3 Bucket to call our Lambda function 
whenever new data arrives.
• Test the setup - Testing S3 Event Trigger to Import New Data into 
DynamoDB
• Cleanup
**Pre-requisites:**
• AWS user account with admin access, not a root account.
• Create an IAM role (For the details and steps on this, follow the PDF I have attached)
