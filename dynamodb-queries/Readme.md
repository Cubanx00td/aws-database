# Querying Data with Amazon DynamoDB

## 🌍 Overview
This project demonstrates how to query data efficiently using Amazon DynamoDB, a managed NoSQL database service provided by AWS. The focus is on creating DynamoDB tables, loading data, running queries using Amazon CLI, and performing transactions.

## 🏗️ Architecture
The project includes:
- Amazon DynamoDB tables with partition and sort keys
- Amazon CLI for querying data
- Transactions to update multiple tables simultaneously

## 🥪 Prerequisites
- AWS Account
- IAM user with permissions to access DynamoDB
- AWS CLI installed and configured

## 🧱 Setup Instructions

### Step 1: Create DynamoDB Tables
1. Open a terminal with AWS CLI configured.
2. Run the following command to create a DynamoDB table:
   ```sh
   aws dynamodb create-table \ 
     --table-name ContentCatalog \ 
     --attribute-definitions AttributeName=id,AttributeType=N \ 
     --key-schema AttributeName=id,KeyType=HASH \ 
     --billing-mode PAY_PER_REQUEST
   ```
3. Verify the table creation using:
   ```sh
   aws dynamodb describe-table --table-name ContentCatalog
   ```

### Step 2: Load Data into DynamoDB
1. Download the sample data:
   ```sh
   curl -O https://storage.googleapis.com/nextwork_course_resources/courses/aws/AWS%20Project%20People%20projects/Project%3A%20Query%20Data%20with%20DynamoDB/nextworksampledata.zip
   ```
2. Extract the downloaded data:
   ```sh
   unzip nextworksampledata.zip
   ```
3. Change to the extracted directory:
   ```sh
   cd nextworksampledata
   ```
4. Use AWS CLI to batch load data:
   ```sh
   aws dynamodb batch-write-item --request-items file://data.json
   ```
5. Verify that the items are successfully added by querying the table.

### Step 3: Query Data with AWS CLI
1. Query a specific item by partition key:
   ```sh
   aws dynamodb query --table-name ContentCatalog --key-condition-expression "id = :id" --expression-attribute-values '{":id": {"N": "202"}}'
   ```
2. Use projection expressions to retrieve specific attributes:
   ```sh
   aws dynamodb query --table-name ContentCatalog --key-condition-expression "id = :id" --expression-attribute-values '{":id": {"N": "202"}}' --projection-expression "Title, ContentType, Services"
   ```

### Step 4: Running Transactions
1. Use transactions to update multiple tables in one operation:
   ```sh
   aws dynamodb transact-write-items --client-request-token TRANSACTION1 --transact-items '[
       {
           "Put": {
               "TableName" : "Comment",
               "Item" : {
                   "Id" : {"S": "Events/Do a Project Together - NextWork Study Session"},
                   "CommentDateTime" : {"S": "2024-9-27T17:47:30Z"},
                   "Comment" : {"S": "Excited to attend!"},
                   "PostedBy" : {"S": "User Connor"}
               }
           }
       },
       {
           "Update": {
               "TableName" : "Forum",
               "Key" : {"Name" : {"S": "Events"}},
               "UpdateExpression": "ADD Comments :inc",
               "ExpressionAttributeValues" : { ":inc": {"N" : "1"} }
           }
       }
   ]'
   ```
2. Ensure all operations succeed or none will be applied.

## 🛠️ Configuration Details
- **DynamoDB Mode:** On-demand or provisioned throughput
- **Keys:** Partition key and optional sort key for efficient querying
- **CLI Tools:** AWS CLI used for inserting and querying data

## 🚨 Troubleshooting

### Common Issues
- **Issue 1:** Query does not return results.
  - **Solution:** Ensure you are using the correct partition key, as it is required for querying.

- **Issue 2:** Transaction failed.
  - **Solution:** Verify that all conditions for the transaction are met and that there are no conflicting writes.

## 🔗 Additional Resources
- [AWS DynamoDB Documentation](https://docs.aws.amazon.com/dynamodb/)
- [AWS CLI Documentation](https://docs.aws.amazon.com/cli/latest/reference/dynamodb/)
- [DynamoDB Best Practices](https://aws.amazon.com/blogs/database/amazon-dynamodb-best-practices/)

This README provides guidance on querying Amazon DynamoDB tables efficiently using AWS CLI and transactions to manage data across multiple tables.

