# AWS CloudFormation Stacks

## Overview
This repository contains two AWS CloudFormation templates for creating AWS resources.

### Stack 1: Comprehensive S3 and EC2 Configuration s3_express_ec2_spot.yaml
This stack creates two S3 buckets (one standard and one S3 Express) and a Spot Instance with an IAM role. The IAM role has full access to perform all actions on both S3 buckets.

#### Features:
- **S3 Standard Bucket**: A general-purpose bucket with a unique name based on the stack parameters.
- **S3 Express Bucket**: Configured for single availability zone data redundancy.
- **EC2 Spot Instance**: Configured with an IAM role that allows unrestricted access to the S3 buckets.

### Stack 2: S3 Express One Zone Configuration s3_express.yaml
This stack focuses on setting up an S3 Express Bucket specifically tailored to operate within a single designated availability zone. It includes an IAM role that provides necessary permissions to access the S3 Express Bucket.

#### Parameters:
- **AvailabilityZone**: The availability zone in which the resources will be created.
- **ExpressBucketPrefix**: Prefix used to name the S3 Express bucket.

#### Resources:
- **OneZoneS3Bucketspeed**: S3 Express bucket configured for a single availability zone.
- **OneZoneBucketPolicy**: Policy granting full access to the S3 Express bucket within the account.

#### Outputs:
- **OneZoneBucketName**: The name of the created S3 Express bucket.

## Troubleshooting Common Issues

### Issue: Access Denied Error
**Error Message**: An error occurred (AccessDenied) when calling the CreateSession operation: Access Denied

**Solution**: Ensure that the IAM policy associated with your resource uses `s3express:*` actions for S3 Express buckets instead of `s3:*` actions. S3 Express buckets have specific action requirements different from general-purpose S3 buckets.

### Issue: Bucket Not Found Error in AWS Lambda
**Error Message**: Trying to get an object from it from an AWS Lambda function in S3 Express One Zone: no such bucket

**Solution**: Adding a layer with the latest version of `boto3` in the AWS Lambda function can resolve this issue. Ensure the bucket name and region are correctly specified in your Lambda function code.

## Conclusion
These templates are designed to simplify the deployment of AWS resources tailored to specific needs, such as data redundancy and resource access within defined availability zones. For any additional questions or support, refer to the AWS CloudFormation and AWS S3 documentation or contact someone from Mars.
