SentimentPulse – Real-Time Sentiment Classification API

Project Overview

This project demonstrates how to deploy a Hugging Face DistilBERT model on AWS SageMaker, expose it via a Lambda function, and make it publicly accessible using API Gateway.

Architecture Summary

| Component        | AWS Service       | Purpose                                         |
|------------------|-------------------|--------------------------------------------------|
| Model Hosting    | SageMaker         | Host DistilBERT as real-time inference endpoint |
| Function Handler | AWS Lambda        | Calls SageMaker endpoint and formats response   |
| API Layer        | API Gateway       | Exposes Lambda as a RESTful HTTP API            |
| Storage          | S3                | Stores pre-trained model and tokenizer files    |
| Permissions      | IAM               | Manages access policies and roles               |
| Monitoring       | CloudWatch        | Logs for Lambda execution and error tracing     |
Model Info

- Model: `distilbert-base-uncased`
- Task: Sentiment classification (positive / negative)
- Framework: Hugging Face Transformers (`transformers==4.26`)
- Files:
  - `pytorch_model.bin`
  - `config.json`
  - `tokenizer_config.json`
  - `vocab.txt`
  - etc.

Deployment Steps

Step 1: Model Preparation
- Download pre-trained DistilBERT using Hugging Face
- Save model & tokenizer into `/model` directory
- Compress the folder (`model.tar.gz`)
- Upload to Amazon S3

Step 2: SageMaker Deployment
- Create a SageMaker notebook
- Register the model using `HuggingFaceModel` class
- Deploy the model to a real-time inference endpoint
- You get a SageMaker endpoint name

Step 3: Lambda Setup
- Create a Lambda function (`Python 3.9`)
- Add SageMaker Full Access policy to Lambda's IAM role
- Write function code to send requests to the endpoint
- Test Lambda with a sample input

Step 4: API Gateway
- Create an HTTP API
- Integrate with the Lambda function
- Define route: `POST /predict`
- Deploy stage: `prod`
-  You receive a public API URL

Sample Inference Test

API Input:
```json
POST /predict
{
  "text": "This product is amazing, I loved it!"
}
```

API Response:
```json
[
  {
    "label": "POSITIVE",
    "score": 0.9996
  }
]
```

Tools & Tech Stack

- AWS SageMaker
- AWS Lambda
- Amazon API Gateway
- Amazon S3
- IAM, CloudWatch
- Python 3.9
- Transformers (HuggingFace)
- PyTorch

Author

ASHISH KUMAR ARIGALA 
MSc Artificial Intelligence & Machine Learning  
University of Limerick