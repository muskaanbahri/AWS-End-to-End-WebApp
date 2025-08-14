
# AWS End to End Web Application
This project demonstrates the integration of five AWS services—Amplify, Lambda, IAM, API Gateway, and DynamoDB—to create and deploy a web application that calculates the power of a given base and exponent. The result of the calculation is stored in a DynamoDB table.
(https://dev.d2u19f69y9k7gd.amplifyapp.com/)

# AWS End to End Web Application
## Architecture

**Amplify** : Used to deploy and host the web application.

**Lambda**: Contains the function that performs the power calculation (base^exponent).

**IAM**: Manages permissions, ensuring secure access to the DynamoDB table for storing results.

**API Gateway**: Creates and manages the POST API that triggers the Lambda function.

**DynamoDB**: Stores the results of the power calculations.

![endtoendarchitecture](https://github.com/muskaanbahri/AWS-End-to-End-WebApp/assets/122555496/e0d24bd4-c5e9-486b-85fe-67b32bd5bbed)







## IAM Execution Policy

```javascript
{
"Version": "2012-10-17",
"Statement": [
    {
        "Sid": "VisualEditor0",
        "Effect": "Allow",
        "Action": [
            "dynamodb:PutItem",
            "dynamodb:DeleteItem",
            "dynamodb:GetItem",
            "dynamodb:Scan",
            "dynamodb:Query",
            "dynamodb:UpdateItem"
        ],
        "Resource": "YOUR-TABLE-ARN"
    }
    ]
}
```

## Lambda function used:

```javascript

import json
import math
import boto3
from time import gmtime, strftime
dynamodb = boto3.resource('dynamodb')
table = dynamodb.Table('powerofmathdb')
now = strftime("%a, %d %b %Y %H:%M:%S +0000", gmtime())

def lambda_handler(event, context):
    mathResult = math.pow(int(event['base']), int(event['exponent']))
    response = table.put_item(
        Item={
            'ID': str(mathResult),
            'LatestGreetingTime':now
            })
    return {
    'statusCode': 200,
    'body': json.dumps('Your result is ' + str(mathResult))
    }
```




## Link for the Web App

[Click here!](https://dev.d2vzk0vjl847d4.amplifyapp.com/)

## Screeshots:
![WhatsApp Image 2024-06-12 at 18 14 24_23d9a873](https://github.com/muskaanbahri/AWS-End-to-End-WebApp/assets/122555496/d5d726af-eed1-4f43-9e27-d01f464e784d)
![WhatsApp Image 2024-06-12 at 18 14 37_1903daae](https://github.com/muskaanbahri/AWS-End-to-End-WebApp/assets/122555496/19124b28-582a-4646-822f-026765f06037)




