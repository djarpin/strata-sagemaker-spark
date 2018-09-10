# Amazon SageMaker Spark Strata tutorial at the 2018 O'Reilly Strata NYC Conference

This repository contains supporting material for the Amazon SageMaker [tutorial](https://conferences.oreilly.com/strata/strata-ny/public/schedule/detail/68909) at the 2018 O'Reilly Strata NYC Conference.

## Setup

1. Log into your AWS account
1. Select EMR from services and create a new cluster:
  1. Go to advanced options
  1. Select Spark and Livy (only)
  1. Click next through the rest (feel free to give a custom name, etc.)
1. Select SageMaker from services and create a SageMaker notebook instance:
  1. Create a new IAM role with access to any S3 bucket
  1. Use the same VPC as your EMR cluster
  1. Take note of security group
1. Return to your EMR cluster
  1. Take note of master node private IP address
  1. Click on the security group for your master node
  1. Add an inbound rule for Custom TCP on port 8998 with the notebook security group as the source
1. Select IAM from services
  1. Select Roles
  1. Select EMR_EC2_DefaultRole
  1. Add AmazonSageMakerFullAccess policy
1. Open your SageMaker notebook instance and start a new terminal and run:
  1. ```echo '{"kernel_python_credentials" : {"url": "http://<emr-master-private-ip>:8998/"}, "session_configs": {"executorMemory": "2g","executorCores": 2,"numExecutors":4}}' > ~/.sparkmagic/config.json```
  1. ```curl <emr-master-private-ip>:8998/sessions```
  1. ```git clone https://github.com/djarpin/strata-sagemaker-spark.git```
