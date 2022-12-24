# Host a basic web application on AWS

In this tutorial, you will build a basic web application. This web application will calculate the remainder between two numbers entered by the user.

## What is a remainder?
- A remainder is the value that is left after the division is completed. For instance, when 25 is divided by 4, the remainder is 1.

# The architecture

<img width="1369" alt="full-stack amplify console arch diagram module 5 8d82fc2a7b47b307dfcefb6fa5f364e8c24426bc" src="https://user-images.githubusercontent.com/50238769/209424802-af9e3b0c-830e-4d28-8b0d-a029dccf506a.png">

The AWS services used in this application are AWS Amplify, Amazon API Gateway, AWS Lambda, Amazon DynamoDB, and AWS Identity and Access Management (IAM).


Some code was re-used from this AWS walk-through:  https://aws.amazon.com/getting-started/hands-on/build-web-app-s3-lambda-api-gateway-dynamodb/

# Module 1 : Create a Web App

In this module, you will use the [AWS Amplify](https://aws.amazon.com/amplify/) to deploy the static resources for your web application. All of your static web content - including HTML, CSS, JavaScript, images, and other files - will be hosted by AWS Amplify. We selected the Amplify service because it makes it straightforward to host and deploy static websites. Your end users will access your site using the URL exposed by Amplify.

## Implementation

### 1. Create a repo on [Github](https://docs.github.com/en/get-started/quickstart/create-a-repo) and upload all your project files to that repo.

