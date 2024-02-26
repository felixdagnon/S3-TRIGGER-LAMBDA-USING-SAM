# 1-S3-trigger-lambda-using-SAM

We continuous with our last demo (Deploying-Serverless-Application-with-AWS-SAM)

in this demo We're going to create an S3 bucket that will trigger our lambda function any time a file is uploaded.

In the template.yaml file, we're going to add additional resources. 

We are going to add additional resources from event souce types  (github page)

```yml
Description: Test Pipeline Lambda
Resources:
  samfunction:
    Type: AWS::Serverless::Function
    Properties:
      Handler: hello_country.lambda_handler
      Runtime: python3.10
      CodeUri: samfunction
      Description: Sample SAM lambda deployment
    Metadata:
      SamResourceId: samfunction
```


Here is the final template  for lambda-events-s3.yml

```yml
AWSTemplateFormatVersion: '2010-09-09'
Transform: 'AWS::Serverless-2016-10-31'
Description: Test Pipeline Lambda
Resources:
  hellofunction:
    Type: 'AWS::Serverless::Function'
    Properties:
      Handler: hello_country.lambda_handler
      Runtime: python3.10
      CodeUri: ./lambda-sam/hello_country.py
      Description: Sample SAM Lambda Deployment
      Events:
        S3Event:
          Type: S3
          Properties:
            Bucket: !Ref S3bucket
            Events: s3:ObjectCreated:*
  S3bucket:
    Type: AWS::S3::Bucket            
```

![image](https://github.com/felixdagnon/S3-TRIGGER-LAMBDA-USING-SAM/assets/91665833/c5737a22-90c9-47dd-b59a-f3b8682c8fa6)


This template lambda-events-s3.yml create unique bucket fur us which will use to trigger lambda

# 2-Create lambda template with SAM

Let's run this package lambda-events-s3.yml:

$ sam package --template-file lambda-events-s3.yml --s3-bucket demotest-101 --output-template-file  lambda-events-s3-packaged.yml

The package is downloaded in SAM directory of Cloud9

![image](https://github.com/felixdagnon/S3-TRIGGER-LAMBDA-USING-SAM/assets/91665833/80822480-ac66-4229-997b-2702f26a2156)

It take the code from local directory and put it in s3 bucket.

Let's check s3 bucket

![image](https://github.com/felixdagnon/S3-TRIGGER-LAMBDA-USING-SAM/assets/91665833/5d2e14c9-23e8-4d5d-b905-f24b1c16d2a7)

# 3-Deploying lambda package with SAM

To deploy the package run the below command

$ sam deploy --template-file lambda-events-s3-packaged.yml --stack-name SAM-S3-events --capabilities CAPABILITY_IAM

The package is done and changeset created in cloudformation

![image](https://github.com/felixdagnon/S3-TRIGGER-LAMBDA-USING-SAM/assets/91665833/e5a2aa26-b720-4816-ae0e-2f05b2ab1150)

Let's see Cloudformation. The stack is created

![image](https://github.com/felixdagnon/S3-TRIGGER-LAMBDA-USING-SAM/assets/91665833/7fd7f55c-50a1-44a3-974a-4b5ef0ff7820)

Let's check in lambda console

![image](https://github.com/felixdagnon/S3-TRIGGER-LAMBDA-USING-SAM/assets/91665833/9aab492e-ec0f-4e20-8bde-13187aba1a02)

Lambda deployment succeed

There is no trigger here but we can check it in S3 bucket

![image](https://github.com/felixdagnon/S3-TRIGGER-LAMBDA-USING-SAM/assets/91665833/1922c5d3-6ac1-48ac-b5f9-c66a533e2f17)


![image](https://github.com/felixdagnon/S3-TRIGGER-LAMBDA-USING-SAM/assets/91665833/ba3bcd0b-7d67-4724-9d58-c538f264b601)


Let's check S3 bucket

Properties

![image](https://github.com/felixdagnon/S3-TRIGGER-LAMBDA-USING-SAM/assets/91665833/a08fab95-b99e-4381-a549-ac3bee5c731b)

scrowl down to "Event notifications"

![image](https://github.com/felixdagnon/S3-TRIGGER-LAMBDA-USING-SAM/assets/91665833/97332493-5c39-4496-933d-8d6c669ee076)


















