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

**The python code do the following:
▪ Imports the CSV file from S3 bucket.
▪ Splits the CSV data into multiple strings.
▪ Uploads data into the DynamoDB table.**

import boto3
s3_client = boto3.client("s3")
dynamodb = boto3.resource("dynamodb")
 
table = dynamodb.Table("FriendsDDB")
 
def lambda_handler(event, context):
    bucket_name = event['Records'][0]['s3']['bucket']['name']
    s3_file_name = event['Records'][0]['s3']['object']['key']
    resp = s3_client.get_object(Bucket=bucket_name,Key=s3_file_name)
    data = resp['Body'].read().decode("utf-8")
    Friends = data.split("\n")
    # print(Friends)
    for friend in Friends:
        print(friend)
        friend_data = friend.split(",")
        # add to dynamodb
        try:
            table.put_item(
                Item = {
                    "Id"        : friend_data[0],
                    "name"      : friend_data[1],
                    "Subject"   : friend_data[2]
                }
            )
        except Exception as e:
            print("End of file")
