## AWS Services
Amazon S3
AWS Lambda
IAM
CloudWatch


##Dependencies
Python 3.x
Boto3
Pillow

Pillow is provided through an AWS Lambda Layer.

##Installation

Install the required dependency locally:

pip install Pillow

Boto3 is already available in the AWS Lambda Python runtime.

##Project Structure
aws-serverless-image-processing/
│
├── lambda_function.py
├── README.md
└── .gitignore
Setup
Create an S3 bucket.
Create input/ and output/ folders.
Create an AWS Lambda function.
Add the Pillow Lambda Layer.
Add the S3 trigger to Lambda.
Configure the Lambda IAM role.
Upload an image to input/.
Check the processed image in output/.
Result

Image upload is automatically processed by Lambda and the output is stored in S3.

Author

Tahir
