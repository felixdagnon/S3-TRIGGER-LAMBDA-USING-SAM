# S3-TRIGGER-LAMBDA-USING-SAM

We continuous with our last demo (Deploying-Serverless-Application-with-AWS-SAM)

in this demo We're going to create an S3 bucket that will trigger our lambda function any time a file is uploaded. 

In the template.yaml file, we're going to add additional resources. 


```json
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

```json
AWSTemplateFormatVersion: '2010-09-09'
Transform: 'AWS::Serverless-2016-10-31'
Description: Test Pipeline Lambda
Resources:
  hellofunction:
    Type: 'AWS::Serverless::Function'
    Properties:
      Handler: hello_country.lambda_handler
      Runtime: python3.10
      CodeUri: ./lambdacode/hello_country.py
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

![image](https://github.com/felixdagnon/S3-TRIGGER-LAMBDA-USING-SAM/assets/91665833/73b15761-a43c-4f04-9fc9-433cfee3b509)




