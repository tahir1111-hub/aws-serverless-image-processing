# 🚀 AWS Serverless Image Processing

A simple serverless image processing project built using **AWS Lambda, Amazon S3, Python, and Pillow**.

## 📌 How It Works

An image is uploaded to the `input/` folder in Amazon S3.

S3 automatically triggers the AWS Lambda function.

Lambda uses **Python and Pillow** to process the image and saves the processed image to the `output/` folder.

CloudWatch is used to monitor Lambda execution logs.

## ☁️ AWS Services Used

- Amazon S3
- AWS Lambda
- AWS IAM
- Amazon CloudWatch

## 💻 Technologies & Dependencies

- Python 3.x
- Boto3
- Pillow

## ⚙️ Setup

### 1. Create S3 Bucket

Create an Amazon S3 bucket and create two folders:

- `input/`
- `output/`

Upload images to the `input/` folder.

### 2. Create Lambda Function

Create an AWS Lambda function with:

- **Runtime:** Python 3.x
- **Handler:** `lambda_function.lambda_handler`

Add the image processing code to the Lambda function.

### 3. Add Pillow Layer

Pillow is required for image processing.

Create a Lambda Layer containing the Pillow library and attach it to the Lambda function.

The Lambda function can then use `from PIL import Image`.

### 4. Configure S3 Trigger

Add an S3 trigger to the Lambda function.

Configure the trigger for **Object Created** events in the `input/` folder.

### 5. Configure IAM Role

Create an IAM execution role for the Lambda function.

Attach the required permissions for:

- Reading objects from the S3 bucket
- Writing processed objects to the S3 bucket
- Writing logs to CloudWatch

The Lambda function uses this IAM role to securely access AWS services without storing AWS access keys in the code.

### 6. Test the Project

Upload an image to the `input/` folder.

S3 automatically triggers Lambda.

Lambda processes the image using Pillow.

The processed image is saved in the `output/` folder.

## 📦 Install Dependencies

For local testing:

`pip install Pillow`

Boto3 is already available in the AWS Lambda Python runtime.

## 🎯 Result

The complete workflow is automated:

**S3 Upload → S3 Trigger → Lambda → Pillow Processing → S3 Output**

## 🔐 Security

AWS credentials are not stored inside the code.

Lambda uses an **IAM execution role** with the required permissions.

For production environments, permissions should follow the **Principle of Least Privilege**.

## 📚 What I Learned

- AWS Lambda
- Amazon S3
- S3 Event Triggers
- IAM Roles & Permissions
- CloudWatch Logs
- Python & Boto3
- Pillow
- Serverless Architecture
- Git & GitHub

## 👨‍💻 Author

**Tahir**

**DevOps & Cloud Learner**
