# 🚀 AWS Serverless Image Processing Pipeline

A serverless image processing pipeline built with **Amazon S3, AWS Lambda, Python, Pillow, IAM, and CloudWatch**.

The project automatically processes an image whenever it is uploaded to an S3 bucket. No continuously running EC2 server is required.

---

## 📸 Project Preview

### Architecture

```text
                         👤 User
                           │
                           │ Upload Image
                           ▼
                  ┌──────────────────┐
                  │    Amazon S3     │
                  │                  │
                  │     input/       │
                  └────────┬─────────┘
                           │
                           │ S3 Event Trigger
                           ▼
                  ┌──────────────────┐
                  │    AWS Lambda    │
                  │                  │
                  │ Python + Pillow  │
                  │                  │
                  │ Process Image    │
                  └────────┬─────────┘
                           │
                           │ Upload Result
                           ▼
                  ┌──────────────────┐
                  │    Amazon S3     │
                  │                  │
                  │     output/      │
                  │                  │
                  │  processed.jpg   │
                  └──────────────────┘

                           │
                           ▼
                  ☁️ Amazon CloudWatch
                     Logs & Monitoring











📌 Project Overview

The purpose of this project is to build an automated serverless image processing system using AWS.

The workflow is:

Upload → S3 → Lambda → Process Image → S3 Output

Whenever an image is uploaded to the input/ folder of the S3 bucket, an S3 event automatically triggers the Lambda function.

The Lambda function downloads the image, processes it using Python and Pillow, converts/saves the result as a JPG image, and uploads it to the output/ folder.

🛠️ AWS Services Used
Service	Purpose
Amazon S3	Store input and output images
AWS Lambda	Run image-processing code
AWS IAM	Manage permissions
Amazon CloudWatch	Logs and monitoring

💻 Technologies Used
Python
Boto3
Pillow
Git
GitHub

⚙️ How I Built This Project
1. Created an S3 Bucket

First, I created an Amazon S3 bucket:

s3-lamda-to

Inside the bucket, I created two folders:

input/
output/

The input/ folder stores the original images.

The output/ folder stores the processed images.

2. Created the Lambda Function

I created an AWS Lambda function using the Python runtime.
The Lambda function is responsible for:
Receiving the S3 event
Identifying the uploaded image
Downloading the image
Processing the image
Saving the processed image
Uploading the result back to S3

3. Added Pillow

Python's Pillow library is used for image processing.
Because Pillow is not included in the basic Lambda runtime, I created and attached a Lambda Layer containing the Pillow dependency.
This allows Lambda to use:
from PIL import Image

4. Connected S3 with Lambda

I configured an S3 event trigger.
The trigger watches the:
input/
folder.
When a new image is uploaded, S3 automatically invokes the Lambda function.

5. Configured IAM Permissions

I created an IAM execution role for the Lambda function.
The role proides the permissions required by Lambda to:
Read the uploaded image from S3
Upload the processed image to S3
Write execution logs to CloudWatch

The project follows the basic Principle of Least Privilege approach instead of putting AWS access keys directly inside the Lambda code.

6. Image Processing

The Lambda function uses Python and Pillow to process the uploaded image.
The image is temporarily stored inside Lambda's:

/tmp

directory.

After processing, the result is saved as a JPG file.

Example:

input/image.png
        ↓
    Lambda
        ↓
output/image.jpg


7. CloudWatch Monitoring

Amazon CloudWatch is used to view Lambda execution logs.
CloudWatch helped me check:

Lambda execution
S3 event information
Errors
Debugging information
Function output
🔄 How the Project Works
Step 1

User uploads:

image.png

to:

S3 → input/
Step 2

S3 detects the new object.

Step 3

S3 sends an event to Lambda.

Step 4

Lambda receives information about the uploaded file.

Step 5

Lambda downloads the image into:

/tmp/
Step 6

Python + Pillow processes the image.

Step 7

The processed image is saved as:

image.jpg
Step 8

Lambda uploads the result to:

S3 → output/
Step 9

CloudWatch records the Lambda execution logs.

📂 S3 Bucket Structure
s3-lamda-to/
│
├── input/
│   └── image.png
│
└── output/
    └── image.jpg
🧠 Lambda Workflow
S3 Event
   ↓
Lambda Handler
   ↓
Read Bucket + Object Key
   ↓
Download Image
   ↓
Pillow Processing
   ↓
Convert / Save as JPG
   ↓
Upload to output/
   ↓
Return Response
🔐 Security

The Lambda function uses an IAM execution role to access AWS services.

AWS credentials are not hard-coded inside the application.

For a production environment, permissions should be restricted to only the required S3 bucket and actions.

🎯 What I Learned

By building this project, I learned:

AWS Lambda fundamentals
Serverless architecture
Amazon S3
S3 event triggers
IAM roles and permissions
CloudWatch logging
Python with Boto3
Image processing with Pillow
Lambda Layers
Git and GitHub
Basic AWS security practices
Connecting multiple AWS services together
🚀 Future Improvements

I plan to extend this project with:

API Gateway
Image upload API
Authentication
More image-processing options
Better error handling
CloudWatch alarms
Automated deployment using CI/CD
📊 Final Architecture
                    ┌─────────────┐
                    │    User     │
                    └──────┬──────┘
                           │
                           │ Upload
                           ▼
                  ┌─────────────────┐
                  │    Amazon S3    │
                  │    input/       │
                  └────────┬────────┘
                           │
                           │ Trigger
                           ▼
                  ┌─────────────────┐
                  │   AWS Lambda    │
                  │                 │
                  │ Python          │
                  │ Boto3           │
                  │ Pillow          │
                  └────────┬────────┘
                           │
                           │ Process
                           ▼
                  ┌─────────────────┐
                  │    Amazon S3    │
                  │    output/      │
                  └─────────────────┘

                           │
                           ▼
                  ┌─────────────────┐
                  │  CloudWatch ☁️  │
                  │ Logs/Monitoring │
                  └─────────────────┘
👨‍💻 Project Status

✅ S3 bucket created
✅ Lambda function created
✅ Pillow Layer configured
✅ S3 → Lambda trigger configured
✅ IAM permissions configured
✅ Image processing implemented
✅ Output stored in S3
✅ CloudWatch logging configured

Status: Completed 🎉

⭐ Author

Tahir

Built as a hands-on AWS & DevOps learning project.
