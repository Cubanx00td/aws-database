# AWS RDS Project

## 🌍 Overview
This project demonstrates how to set up and use Amazon RDS (Relational Database Service) with MySQL. The goal is to create an RDS instance, populate it with data using MySQL Workbench, and visualize the data with Amazon QuickSight.

## 🏗️ Architecture
Amazon RDS provides a scalable, managed relational database service. The architecture includes:
- Amazon RDS instance
- MySQL Workbench for database management
- Amazon QuickSight for data visualization

## 🥪 Prerequisites
- AWS Account
- IAM user with sufficient permissions
- Amazon RDS instance (MySQL)
- MySQL Workbench
- Amazon QuickSight

## 🧱 Setup Instructions

### Step 1: Create an Amazon RDS Instance
1. Log in to your AWS Management Console.
2. Navigate to the RDS service.
3. Click on "Create database" and choose MySQL as the engine.
4. Configure database settings and credentials.
5. Ensure that the database is public if you need to access it externally.

### Step 2: Configure Security Group for Remote Access
1. Navigate to the EC2 Security Groups.
2. Modify the security group associated with the RDS instance.
3. Add an inbound rule to allow traffic from your IP address.

### Step 3: Connect to the RDS Instance using MySQL Workbench
1. Open MySQL Workbench.
2. Create a new connection using the RDS endpoint, username, and password.
3. Connect and create a schema with tables.
4. Insert sample data using SQL queries.

### Step 4: Connect Amazon QuickSight to RDS
1. Open Amazon QuickSight.
2. Create a new dataset and select RDS as the data source.
3. Provide RDS credentials and validate the connection.
4. Secure the RDS instance by restricting access to only the QuickSight security group.

## 🛠️ Configuration Details
- **Database Engine:** MySQL
- **Instance Type:** Configurable based on workload
- **Public Access:** Initially enabled for setup, later secured
- **Security:** Uses security groups to restrict access

## 🚨 Troubleshooting

### Common Issues
- **Issue 1:** Unable to connect to RDS instance.
  - **Solution:** Ensure that the security group allows inbound traffic from your IP address.

- **Issue 2:** Data not appearing in QuickSight.
  - **Solution:** Verify that the RDS instance is accessible from QuickSight by updating the VPC connection settings.

## 🔗 Additional Resources
- [AWS RDS Documentation](https://docs.aws.amazon.com/rds/)
- [MySQL Workbench Documentation](https://dev.mysql.com/doc/workbench/en/)
- [Amazon QuickSight Documentation](https://docs.aws.amazon.com/quicksight/)

This README provides a structured approach to setting up and using Amazon RDS efficiently while ensuring security and scalability.

