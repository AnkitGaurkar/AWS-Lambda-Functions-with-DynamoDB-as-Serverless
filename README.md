🚀 AWS_Lambda_Function_With_DynamoDB (Serverless)

This project demonstrates how to build a serverless backend using AWS Lambda and Amazon DynamoDB to insert and fetch data without managing servers..

☁️ AWS Services Used

⚡ AWS Lambda – Executes backend logic
🗄️ Amazon DynamoDB – NoSQL database
🔐 AWS IAM – Permissions & security
📊 Amazon CloudWatch – Logs & monitoring

📚 Definitions

AWS Lambda
A serverless compute service that runs code only when triggered.

DynamoDB
A fully managed NoSQL database to store application data.

IAM
Controls access between AWS services.

CloudWatch
Stores logs and helps debug Lambda functions.

🧩 Architecture

Client / Test Event → AWS Lambda → DynamoDB

🗄 DynamoDB Table Design

Table Name: Learners

Attributes
learner_id (Number – Primary Key)
RollNo (String)
name (String)

Example
learner_id = 1
RollNo = A123
name = Ankit

🛠 Step-by-Step Setup

1️⃣ Create DynamoDB Table
Go to AWS Console → DynamoDB → Create table
Table Name = Learners
Partition Key = learner_id (Number)
Click Create

2️⃣ Create Lambda – Insert Data
AWS Console → Lambda → Create function
Name = insert-learner
Runtime = Python
Attach IAM Policy = AmazonDynamoDBFullAccess

Insert Lambda Code
import boto3
dynamodb = boto3.resource('dynamodb')
table = dynamodb.Table('Learners')

def lambda_handler(event, context):
  table.put_item(Item={
   "learner_id": int(event["learner_id"]),
   "RollNo": event["RollNo"],
   "name": event["name"]
  })
  return "Data inserted successfully"

Insert Test Input
learner_id = 1
RollNo = A123
name = Ankit

Insert Output
Data inserted successfully

3️⃣ Create Lambda – Fetch Data
Create new Lambda → fetch-learner
Attach DynamoDB permission

Fetch Lambda Code
import boto3
dynamodb = boto3.resource('dynamodb')
table = dynamodb.Table('Learners')

def lambda_handler(event, context):
  response = table.get_item(Key={"learner_id": int(event["learner_id"])})
  return response.get("Item", "Learner not found")

Fetch Test Input
learner_id = 1

Fetch Output
learner_id = 1
RollNo = A123
name = Ankit

❌ Error Scenarios

If learner_id is missing → learner_id is required
If learner_id is not found → Learner not found

🧠 What This Project Demonstrates

✔ Serverless backend with AWS Lambda
✔ NoSQL data storage using DynamoDB
✔ IAM-based security
✔ CloudWatch logging
✔ Event-driven cloud workflow

📄 Resume-Ready Line

Built a serverless backend using AWS Lambda and DynamoDB to insert and fetch data with secure IAM permissions and cloud-based logging.
