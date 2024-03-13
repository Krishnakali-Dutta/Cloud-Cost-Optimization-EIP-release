# AWS Lambda Function by Releasing Elastic IPs

This repository contains code for an AWS Lambda function written in Python that releases unassociated Elastic IP (EIP) addresses in your AWS account.

## Overview

Elastic IPs are static public IP addresses that can be associated with various AWS resources such as EC2 instances, NAT Gateways, load balancers, and more. This Lambda function automates the process of releasing Elastic IPs that are not currently associated with any resource, helping to optimize costs and resource usage in your AWS environment.

## Functionality

The Lambda function retrieves a list of all Elastic IP addresses in your AWS account using the Boto3 SDK for Python. It then iterates through the list and releases any Elastic IPs that are not associated with any resource.

## Usage

1. Clone or download this repository to your local machine.
2. Navigate to the directory and execute the following AWS CLI command to create your lambda function:

aws lambda create-function --function-name Eip_release --zip-file file://lambda_function.py.zip --handler lambda_handler --role "Your-IAM-role" --runtime python3.8

3. Create an IAM role with permissions by using policies given below to describe and release Elastic IPs.
4. Replace the IAM role created in the CLI command in step 2 to associate it with the Lambda function.
5. configure a trigger for the Lambda function (e.g., CloudWatch Events) to automate the process of releasing unassociated Elastic IPs.

## IAM Policy

Ensure that the IAM role associated with the Lambda function has the necessary permissions to describe and release Elastic IPs. Here's an example IAM policy:


```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "ec2:DescribeAddresses",
                "ec2:ReleaseAddress"
            ],
            "Resource": "*"
        }
    ]
}

