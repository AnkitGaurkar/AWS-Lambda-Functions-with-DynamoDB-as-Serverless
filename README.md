🚀 AWS Lambda + DynamoDB – Serverless Learner Management System

This project shows how to build a serverless backend using AWS Lambda and Amazon DynamoDB to store and fetch learner data.

☁️ AWS Resources Used

⚡ AWS Lambda – Backend logic

🗄️ Amazon DynamoDB – Database

🔐 AWS IAM – Security permissions

📊 Amazon CloudWatch – Logs

📚 Definitions

⚡ AWS Lambda – Runs code without servers

🗄️ DynamoDB – NoSQL cloud database

🔐 IAM – Controls access to AWS services

📊 CloudWatch – Shows Lambda logs

🧩 Architecture
Client → AWS Lambda → DynamoDB

🗄️ DynamoDB Table

Table Name: Learners

Fields

🔑 learner_id (Number – Primary Key)

📄 RollNo (String)

👤 name (String)

🛠️ Step-by-Step Setup
1️⃣ Create DynamoDB Table

Go to AWS Console → DynamoDB → Create table

Name: Learners

Partition Key: learner_id (Number)

Click Create

2️⃣ Create Insert Lambda

Go to AWS Console → Lambda → Create function

Name: insert-learner

Runtime: Python

Attach IAM policy: AmazonDynamoDBFullAccess

Insert Lambda Code

import boto3
table = boto3.resource('dynamodb').Table('Learners')

def lambda_handler(event, context):
    table.put_item(Item={
        "learner_id": int(event["learner_id"]),
        "RollNo": event["RollNo"],
        "name": event["name"]
    })
    return "Inserted"


Insert Test Input

learner_id = 1
RollNo = A123
name = Ankit

3️⃣ Create Fetch Lambda

Create new Lambda → fetch-learner

Attach DynamoDB permission

Fetch Lambda Code

import boto3
table = boto3.resource('dynamodb').Table('Learners')

def lambda_handler(event, context):
    res = table.get_item(Key={"learner_id": int(event["learner_id"])})
    return res.get("Item", "Not found")


Fetch Test Input

learner_id = 1


Fetch Output

learner_id = 1
RollNo = A123
name = Ankit

❌ Error Scenarios

Missing learner_id → learner_id is required

Wrong learner_id → Not found

🧠 What This Project Shows

✔ Serverless backend

✔ DynamoDB integration

✔ IAM security

✔ CloudWatch logging

✔ Real cloud workflow

📄 Resume Line

Built a serverless backend using AWS Lambda and DynamoDB to store and retrieve learner data with secure IAM permissions and cloud-based logging.
