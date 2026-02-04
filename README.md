📘 AWS Lambda + DynamoDB – Serverless Learner Management System

This project demonstrates how to build a serverless backend using AWS Lambda and Amazon DynamoDB to store and retrieve learner information.

☁️ Cloud Platform

Built on Amazon Web Services (AWS)

Services used:

AWS Lambda

Amazon DynamoDB

AWS IAM

Amazon CloudWatch

📚 Definitions
AWS Lambda

AWS Lambda is a serverless compute service that runs your code without managing servers.

DynamoDB

DynamoDB is a fully managed NoSQL database used to store application data.

IAM

IAM controls which AWS services can access other AWS services.

CloudWatch

CloudWatch stores logs and helps debug AWS Lambda.

🧩 Architecture
Client / Test Event
        |
        v
   AWS Lambda
        |
        v
 Amazon DynamoDB

🗄 DynamoDB Table

Table Name: Learners

Attribute	Type
learner_id	Number (Primary Key)
RollNo	String
name	String
🔹 Lambda 1 – Insert Data
Purpose

Store learner data in DynamoDB.

Code
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

Test Event
{
  "learner_id": 1,
  "RollNo": "A123",
  "name": "Ankit"
}

🔹 Lambda 2 – Fetch Data
Purpose

Retrieve learner data using learner_id.

Code
import boto3

dynamodb = boto3.resource('dynamodb')
table = dynamodb.Table('Learners')

def lambda_handler(event, context):
    response = table.get_item(
        Key={"learner_id": int(event["learner_id"])}
    )
    return response.get("Item", "Learner not found")

Test Event
{
  "learner_id": 1
}

🟢 Output
{'learner_id': Decimal('1'), 'RollNo': 'A123', 'name': 'Ankit'}

❌ Error Cases
Scenario	Result
Missing learner_id	Error
learner_id not found	Learner not found
🧠 What This Project Shows
Skill	Description
Serverless computing	AWS Lambda
NoSQL database	DynamoDB
Cloud security	IAM
Debugging	CloudWatch
Backend API	JSON input/output
📄 Resume-Ready Line

Built a serverless backend using AWS Lambda and DynamoDB to store and retrieve learner data with secure IAM permissions and cloud-based logging.
