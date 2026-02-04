🚀 AWS_Lambda_Function_With_DynamoDB (Serverless)

This project demonstrates how to build a serverless backend using AWS Lambda and Amazon DynamoDB to insert and fetch data without managing any servers.

It reflects a real-world event-driven cloud architecture used in modern applications.

☁️ AWS Services Used
Service	Purpose
⚡ AWS Lambda	Executes backend logic
🗄️ Amazon DynamoDB	NoSQL database
🔐 AWS IAM	Permissions & security
📊 Amazon CloudWatch	Logs & monitoring
📚 Definitions

AWS Lambda
A serverless compute service that runs code only when triggered.

DynamoDB
A fully managed NoSQL database with high availability and scalability.

IAM
Controls access between AWS services.

CloudWatch
Stores logs and helps debug Lambda functions.

🧩 Architecture
Client / Test Event
        |
        v
   AWS Lambda
        |
        v
 Amazon DynamoDB

🗄 DynamoDB Table Design

Table Name: Learners

Attribute	Type	Description
learner_id	Number	Primary Key
RollNo	String	Roll number
name	String	Learner name

Example item:

learner_id = 1
RollNo = A123
name = Ankit

🛠 Step-by-Step Setup
1️⃣ Create DynamoDB Table

AWS Console → DynamoDB → Create table

Table name: Learners

Partition key: learner_id (Number)

Click Create

2️⃣ Create Lambda Function – Insert Data

Function Name: insert-learner
Runtime: Python
IAM Policy: AmazonDynamoDBFullAccess

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

Output
Data inserted successfully

3️⃣ Create Lambda Function – Fetch Data

Function Name: fetch-learner
Runtime: Python
IAM Policy: AmazonDynamoDBFullAccess

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

Output
{
  "learner_id": 1,
  "RollNo": "A123",
  "name": "Ankit"
}

❌ Error Scenarios
Scenario	Result
learner_id missing	learner_id is required
learner_id not found	Learner not found
🧠 What This Project Demonstrates

Serverless backend using AWS Lambda

NoSQL data storage with DynamoDB

IAM-based security

CloudWatch logging

Event-driven cloud workflow

📄 Resume-Ready Description

Built a serverless backend using AWS Lambda and DynamoDB to insert and fetch data with secure IAM permissions and cloud-based logging.
