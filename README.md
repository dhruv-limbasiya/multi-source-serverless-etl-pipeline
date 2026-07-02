# 🌍 multi-source-serverless-etl-pipeline

A production-style **Serverless ETL Pipeline** built using **AWS Lambda, Amazon S3, DynamoDB, CodePipeline, CodeBuild, and GitHub Actions**.

The project automatically processes multiple file formats uploaded to Amazon S3 and loads cleaned data into DynamoDB tables through an event-driven architecture.

---

# 📌 Project Overview

This project demonstrates a complete serverless data engineering workflow.

Whenever a file is uploaded to Amazon S3:

- S3 triggers the appropriate AWS Lambda function.
- Lambda parses the uploaded file.
- Data is validated and transformed.
- Clean records are stored in DynamoDB.
- CloudWatch stores execution logs.
- GitHub + CodePipeline + CodeBuild automatically deploy code changes.

The project currently supports three independent ETL pipelines:

- 🌍 Earthquake JSON
- 🌦 Weather JSON
- 👨‍💼 Employee CSV

---

# 🏗 Architecture

```
                    Git Push
                       │
                       ▼
                  GitHub Repository
                       │
                       ▼
                 GitHub Webhook
                       │
                       ▼
                 AWS CodePipeline
                       │
                       ▼
                  AWS CodeBuild
                       │
      ┌────────────┬─────────────┬─────────────┐
      ▼            ▼             ▼
 Earthquake     Weather      Employee
    Lambda       Lambda        Lambda
      │            │             │
      ▼            ▼             ▼
 Validation   Validation   Validation
      │            │             │
      ▼            ▼             ▼
 Transformation Transformation Transformation
      │            │             │
      ▼            ▼             ▼
 DynamoDB      DynamoDB      DynamoDB
      │            │             │
      └────────────┴─────────────┘
                   │
                   ▼
             CloudWatch Logs
```

---

# 📂 Project Structure

```
earthquake-serverless-etl/

│
├── earthquake/
│   ├── config/
│   ├── loaders/
│   ├── parsers/
│   ├── transform/
│   ├── utils/
│   ├── fetch_data.py
│   └── lambda_function.py
│
├── weather/
│   ├── loaders/
│   ├── parsers/
│   ├── transform/
│   ├── weather_fetch.py
│   └── lambda_function.py
│
├── employee/
│   ├── loaders/
│   ├── parsers/
│   ├── transform/
│   └── lambda_function.py
│
├── sampleData/
│   ├── earthquake.json
│   ├── weather.json
│   └── employee.csv
│
├── screenshots/
│
├── .github/
│   └── workflows/
│
├── buildspec.yml
├── requirements.txt
└── README.md
```

---

# 🚀 Features

## Earthquake Pipeline

- Reads JSON files
- Validates earthquake records
- Calculates earthquake severity
- Converts timestamps
- Stores records in DynamoDB

---

## Weather Pipeline

- Reads weather JSON
- Extracts

  - Temperature
  - Wind Speed
  - Timestamp

- Stores latest weather record

---

## Employee Pipeline

- Reads CSV
- Validates employee records
- Cleans employee data
- Stores employee information

---

# ☁ AWS Services Used

- AWS Lambda
- Amazon S3
- Amazon DynamoDB
- Amazon CloudWatch
- AWS IAM
- AWS CodePipeline
- AWS CodeBuild

---

# 💻 Technologies

- Python 3.11
- boto3
- JSON
- CSV
- Git
- GitHub
- GitHub Actions

---

# 📦 Supported Input Files

## Earthquake

```
JSON
```

Uploaded to:

```
raw/earthquake/
```

---

## Weather

```
JSON
```

Uploaded to:

```
raw/weather/
```

---

## Employee

```
CSV
```

Uploaded to:

```
raw/employee/
```

---

# 📊 DynamoDB Tables

The project stores processed data inside three tables.

| Table | Description |
|--------|-------------|
| earthquake_records | Earthquake information |
| weather_records | Weather information |
| employee_records | Employee information |

---

# ⚙ ETL Workflow

## Extract

- Read uploaded file from Amazon S3

---

## Transform

- Validate records
- Remove invalid data
- Standardize fields
- Calculate derived values

---

## Load

- Store processed records into DynamoDB

---

# 🔄 CI/CD Pipeline

The deployment process is fully automated.

```
Git Push

↓

GitHub

↓

CodePipeline

↓

CodeBuild

↓

Build Lambda ZIPs

↓

Deploy to AWS Lambda
```

Every push to the **master** branch automatically deploys all Lambda functions.

---

# 📁 Event Notifications

| Folder | Trigger |
|----------|---------|
| raw/earthquake/ | Earthquake Lambda |
| raw/weather/ | Weather Lambda |
| raw/employee/ | Employee Lambda |

---

# 📈 Logging

CloudWatch Logs records:

- Uploaded filename
- Total records
- Successful inserts
- Failed records
- Execution time
- Errors

---

# 🧪 Testing

Upload sample files into S3.

```
raw/earthquake/earthquake.json
```

```
raw/weather/weather.json
```

```
raw/employee/employee.csv
```

The appropriate Lambda function will execute automatically.

---

# Future Improvements

- Step Functions
- EventBridge
- SNS Notifications
- SQS Dead Letter Queue
- AWS Glue
- Amazon Athena
- Terraform
- AWS CDK
- Unit Testing
- Docker Support

---

# Learning Outcomes

This project demonstrates practical experience with:

- Event-Driven Architecture
- Serverless ETL
- AWS Lambda
- Amazon S3
- DynamoDB
- CloudWatch
- IAM
- CI/CD Pipelines
- GitHub Actions
- CodePipeline
- CodeBuild
- Python
- Data Validation
- Data Transformation

---

# Author

**Dhruv Limbasiya**

GitHub:

https://github.com/dhruv-limbasiya
