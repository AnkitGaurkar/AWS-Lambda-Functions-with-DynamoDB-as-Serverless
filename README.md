# AWS-Lambda-Functions-with-DynamoDB-as-Serverless

📘 AWS Lambda + DynamoDB – Serverless Learner Management System

This project demonstrates how to build a serverless backend system using AWS Lambda and Amazon DynamoDB to store and retrieve learner information.

This type of architecture is widely used in real-world web and mobile applications.

☁️ Cloud Platform

Built on Amazon Web Services (AWS)

Services used:

Service	Purpose
AWS Lambda	Runs backend code without servers
Amazon DynamoDB	Stores learner data
AWS IAM	Controls security and permissions
Amazon CloudWatch	Stores logs and errors
📚 Definitions (Very Important)
🔹 AWS Lambda

AWS Lambda is a serverless compute service that lets you run code without managing servers.
You just upload code and AWS runs it automatically when called.

🔹 DynamoDB

DynamoDB is a fully managed NoSQL database.
It stores data in tables, and each record is called an item.

🔹 IAM

IAM controls who can access what.
Lambda needs permission to read/write DynamoDB.

🔹 CloudWatch

CloudWatch is AWS’s logging and monitoring service.
All Lambda logs go here.

🧩 Architecture
Client / Test Event
        |
        v
   AWS Lambda
        |
        v
 Amazon DynamoDB

🗄 DynamoDB Table Structure

Table Name: Learners

Attribute	Type
learner_id	Number (Primary Key)
RollNo	String
name	String

Example:

learner_id	RollNo	name
1	A123	Ankit
🔹 Step-by-Step Setup
Step 1 — Create DynamoDB Table

Go to AWS Console → DynamoDB

Click Create table

Table name: Learners

Partition key: learner_id (Number)

Click Create table

Step 2 — Create Lambda for Insert

Go to AWS Lambda → Create function

Name: insert-learner

Runtime: Python

Click Create

Give it permission: Attach AmazonDynamoDBFullAccess

Insert Lambda Code
import boto3

dynamodb = boto3.resource('dynamodb')
table = dynamodb.Table('Learners')

def lambda_handler(event, context):
    table.put_item(
        Item={
            "learner_id": int(event["learner_id"]),
            "RollNo": event["RollNo"],
            "name": event["name"]
        }
    )
    return "Data inserted successfully"

Test Event (Insert)
{
  "learner_id": 1,
  "RollNo": "A123",
  "name": "Ankit"
}

Step 3 — Create Lambda for Fetch

Create another Lambda: fetch-learner

Give it DynamoDB permission

Fetch Lambda Code
import boto3

dynamodb = boto3.resource('dynamodb')
table = dynamodb.Table('Learners')

def lambda_handler(event, context):
    response = table.get_item(
        Key={"learner_id": int(event["learner_id"])}
    )
    return response.get("Item", "Learner not found")

Test Event (Fetch)
{
  "learner_id": 1
}

🟢 Output
{'learner_id': Decimal('1'), 'RollNo': 'A123', 'name': 'Ankit'}

❌ Error Scenarios
Case	Input	Output
No ID	{}	Error
Wrong ID	{ "learner_id": 99 }	Learner not found
🧠 What This Project Shows
Skill	Explanation
Serverless computing	Using Lambda
Database design	DynamoDB
Cloud security	IAM
Debugging	CloudWatch
Backend API	JSON input/output
📄 Resume-Ready Line

Built a serverless backend using AWS Lambda and DynamoDB to store and retrieve learner data with secure IAM permissions and cloud-based logging.
