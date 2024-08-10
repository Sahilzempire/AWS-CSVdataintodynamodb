AWS Data Engineering projects.
Welcome to Project 1 in AWS Data engineering projects series.(Download RAW file, if file showing any error)

This is basic level Data Engg project that aims to "**To import CSV data into DynamoDB using Lambda and S3 Event Triggers**"

This is a readme file that is going to provide you summary about the Project. I have attached a doc file that involves all the details about the services being used and also the steps used to achieve our goal. I have also attached 2 CSV files that I have used in this project and you can change the file or create your own but remember file format should be .csv as the project is for that only.

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

**CONCLUSION:-**
The project "To import CSV data into DynamoDB using Lambda and S3 Event Triggers" has successfully demonstrated the power and flexibility of AWS services. 

By leveraging **AWS Lambda** and **S3 Event Triggers**, we have created an automated pipeline that imports CSV data into a **DynamoDB** table. This not only simplifies the data import process but also makes it more efficient and reliable. 

The use of **S3 Event Triggers** allows for real-time data processing as soon as the CSV file is uploaded to the S3 bucket. This eliminates the need for manual intervention and ensures that the DynamoDB table is always up-to-date with the latest data.

The **Lambda function** serves as the backbone of this project, handling the task of reading the CSV file and writing the data to the DynamoDB table. This serverless computing service is cost-effective as it only runs when triggered, and scales automatically to handle the size of the incoming data.

In conclusion, this project has effectively utilized AWS services to create a robust and scalable data import solution. It highlights the potential of cloud computing in handling large datasets and automating data workflows. Future improvements could include error handling mechanisms and optimization of the Lambda function for faster data processing. This project serves as a strong foundation for any data-driven application that requires real-time, reliable, and scalable data import functionality.
