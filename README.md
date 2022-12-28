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

###  Create a repo on Github

 - Create your repo on [Github](https://docs.github.com/en/get-started/quickstart/create-a-repo) and upload all your project files to that repo.

### Create a web with Amplify console
- In a new browser window, log into the [Amplify console](https://us-east-1.console.aws.amazon.com/amplify/home?region=us-east-1#/). Note: We will be using the N. Virginia (us-east-1) Region for this tutorial.
- In the **Get Started** section, under **Host your web app**, choose the orange **Get started** button.
- Select **GitHub**. This is what you should see on the screen:

![Screenshot 2022-12-24 at 09 14 18](https://user-images.githubusercontent.com/50238769/209425599-e8f1eb76-69ea-4acc-b6bc-8757a97501db.png)

- Choose the **Continue** button and authenticate and authorise your GitHub account when prompted.
- Select your Repo in the dropdown and click the **Next** button. This is what you should see on the screen. 

# Come back and confirm if selecting the tick box is correct
![Screenshot 2022-12-24 at 09 17 24](https://user-images.githubusercontent.com/50238769/209425757-02d44455-b02d-4994-890b-508a7fc178f4.png)

- Select **continue**, then choose the **Save and deploy** button. After a few seconds, you should see the message *Deployment successfully completed*.

### Test your web application
- Select **Domain Management** in the left navigation menu.
- Copy and paste the URL displayed in the form into your browser.


# Module 2: Create a Lambda function

In this module, you will be writing a small piece of code in Python to be used in your web application.You will use [AWS Lambda](https://aws.amazon.com/lambda/?e=gs2020&p=build-a-web-app-two), a compute service that lets you create serverless functions, eliminating the need for you to manage software and hardware. Instead, applications are broken up into individual functions that can be invoked and scaled individually.


## Implementation

### Create and configure your Lambda function

- In a new browser tab, log in to the [AWS Lambda console](https://us-east-1.console.aws.amazon.com/lambda/home?region=us-east-1#/functions).
- Make sure you create your **function in the same Region in which you created the web app in the previous module**. You can see this at the very top of the page, next to your account name.
- Choose the orange **Create function** button.
- Under **Function name**, enter *RemainderFunction*.
- Select **Python 3.8** from the **runtime** dropdown and leave the rest of the defaults unchanged.

![Screenshot 2022-12-24 at 09 49 59](https://user-images.githubusercontent.com/50238769/209426597-e7c07a2b-f8cc-4f70-a4c2-dd412222f83b.png)

- Choose the orange **Create function** button.
- You should see a green message box at the top of your screen with the following message "Successfully created the function **RemainderFunction**."
- Under **Code source**, replace the code in **lambda_function.py** with the following:


![Screenshot 2022-12-24 at 09 54 53](https://user-images.githubusercontent.com/50238769/209426682-99ad00bd-7284-43ef-812f-0321cc24334e.png)

- Save by going to the file menu and selecting **Save** to save the changes.
- Choose **Deploy** to deploy the changes.
-  Choose the orange **Test** button to create a test event by selecting **Configure test event**.


![Screenshot 2022-12-24 at 09 59 01](https://user-images.githubusercontent.com/50238769/209426795-e74bb9d5-41a2-4313-8e3c-762cd26e9c94.png)

- Under **Event name**, enter *RemainderTestEvent*.
- Copy and paste the following JSON object to replace the default one:

![Screenshot 2022-12-24 at 13 33 06](https://user-images.githubusercontent.com/50238769/209434084-9de4511f-b0fd-4eba-a20a-f25bffed7635.png)




-  Choose the orange **Create** button at the bottom of the page.


# Module 3: Link a Serverless Function to your Web App
In this module, we will use [Amazon API Gateway](https://aws.amazon.com/api-gateway/?e=gs2020&p=build-a-web-app-three) to create a RESTful API that will allow us to make calls to our Lambda function from a web client (typically refers to a user's web browser). API Gateway will act as a middle layer between the HTML client we created in module one and the serverless backend we created in module two.

## Implementation

### Create REST API

- Login to the [API Gateway console](https://us-east-1.console.aws.amazon.com/apigateway/main/apis?region=us-east-1)
- In the **Choose an API type** section, find the REST API card and choose the **Build** button on the card.
- Under **Choose the protocol**, select **REST**.
- Under **Create new API**, select **New API**.
- In the **API name** field, enter RemainderAPI.
- Select **Edge optimized*8 from the **Endpoint Type** dropdown. 
- Choose the blue **Create API** button. Your settings should look like the accompanying screenshot.

![Screenshot 2022-12-24 at 12 58 23](https://user-images.githubusercontent.com/50238769/209433022-84d6d3d1-6bb1-4733-9960-0c40d0784472.png)


### Create a new resource and method

- In the left navigation pane, select **Resources** under **API: HelloWorldAPI**.
- Ensure the "/" resource is selected.
- From the **Actions** dropdown menu, select **Create Method**.
- Select **POST** from the new dropdown that appears, then select the checkmark.
- Select **Lambda Function** for the **Integration type**.
- Select the **Lambda Region** you used when making the function (or else you will see a warning box reading "You do not have any Lambda Functions in...").
- Enter *RemainderFunction* in the **Lambda Function** field.
- Choose the blue **Save** button.
- You should see a message letting you know you are giving the API you are creating permission to call your Lambda function. Choose the **OK** button.
- With the newly created POST method selected, select **Enable CORS** from the **Action** dropdown menu.
- Leave the POST checkbox selected and choose the blue **Enable CORS and replace existing CORS headers** button.


<img width="896" alt="Full Stack tutorial ConfirmMethodChanges 06ab437c86819e780eacc2bb2d5847d8f6274648" src="https://user-images.githubusercontent.com/50238769/209433359-e3ca04be-748f-43d2-9432-8b02e2c34cde.png">


- You should see a message asking you to confirm method changes. Choose the blue **Yes, replace existing values** button.


<img width="939" alt="Full Stack tutorial EnableCORS 5bd0a1c5540ba714abe44a6ffa0c80a3dd58ce16" src="https://user-images.githubusercontent.com/50238769/209433362-3e295934-be6d-4757-a198-8a2865217b20.png">


### Deploy API

- In the Actions dropdown list, select **Deploy API**.
- Select **[New Stage]** in the **Deployment stage** dropdown list.
- Enter dev for the **Stage Name**.
- Choose **Deploy**.
- Copy and save the URL next to **Invoke URL** (you will need it in module five).


![Screenshot 2022-12-24 at 13 24 38](https://user-images.githubusercontent.com/50238769/209433697-aa674e5c-14c8-4e57-9001-13f57660e438.png)


### Validate API
- In the left navigation pane, select **Resources**.
- The methods for our API will now be listed on the right. Choose **POST**.
- Choose the small blue lightning bolt.
- Paste the following into the **Request Body** field:



![Screenshot 2022-12-24 at 13 35 02](https://user-images.githubusercontent.com/50238769/209434152-6953c7ac-e2ee-4177-b5df-5633a3ef1dbb.png)



- Choose the blue **Test** button.
- On the right side, you should see a response with **Code 200.

![Screenshot 2022-12-24 at 13 35 35](https://user-images.githubusercontent.com/50238769/209434165-382e8875-6ca5-4125-8be7-cecbd90dfcdf.png)


# Module 4 : Create a Data Table
In this module, you will create an [Amazon DynamoDB](https://aws.amazon.com/dynamodb/?e=gs2020&p=build-a-web-app-four) table and enable your Lambda function to store data in it. Additionally, we will use the [AWS Identity and Access Management (IAM) service](https://aws.amazon.com/iam/?e=gs2020&p=build-a-web-app-four) to securely give our services the required permissions to interact with each other. Specifically, we are going to allow the Lambda function we created in module two to write to our newly created DynamoDB table using an IAM policy.


## Implementation

### Create a DynamoDB table

- Log in to the Amazon [DynamoDB console].(https://us-east-1.console.aws.amazon.com/dynamodbv2/home?region=us-east-1)
- Make sure you create your table in the same Region in which you created the web app in the previous module. You can see this at the very top of the page, next to your account name.
- Choose the orange **Create table** button.
- Under **Table name**, enter RemainderDatabase.
- In the **Partition key** field, enter ID. The partition key is part of the table's primary key.
- Leave the rest of the default values unchanged and choose the orange **Create table** button.
- In the list of tables, select the table name, *RemainderDatabase.
- In the **General information** section, show **Additional info** by selecting the down arrow.
- Copy the **Amazon Resource Name (ARN)**. You will need it later in this module.

### Create and add IAM policy to Lambda function

- Now that we have a table, let's edit our Lambda function to be able to write data to it. In a new browser window, open the [AWS Lambda console](Now that we have a table, let's edit our Lambda function to be able to write data to it. In a new browser window, open the AWS Lambda console).
- Select the function we created in module two (RemainderFunction). Note: We are using the N. Virginia (us-east-1) Region for this tutorial.
- We'll be adding permissions to our function so it can use the DynamoDB service, and we'll be using AWS Identity and Access Management (IAM) to do so.
- Select the **Configuration** tab and select **Permissions** from the right side menu.
- In the **Execution role** box, under **Role name**, choose the link. A new browser tab will open.
- In the **Permissions policies** box, open the **Add permissions** dropdown and select **Create inline policy**.
- Select the **JSON** tab.
- Paste the following policy in the text area, taking care to replace your table's ARN in the Resource field in line 15:

### Please note: It would be simpler to simply add the dynamoDb full access policy 'AmazonDynamoDBFullAccess', which provides full access to Amazon DynamoDB via the AWS Management Console, but due to IAM security best practices, we will use least-privilege permission, which means that when you set permissions with IAM policies, grant only the permissions required to perform a task.

![Screenshot 2022-12-28 at 14 56 28](https://user-images.githubusercontent.com/50238769/209815827-06baea3a-4dcb-45a8-a7a6-c8a82cea143a.png)

- This policy will allow our Lambda function to read, edit, or delete items, but restrict it to only be able to do so in the table we created.
-  Choose the blue **Review Policy** button.
-  Next to Name, enter *RemainderAppDynamoPolicy.
-  Choose the blue **Create Policy** button.


## Test the changes

- Test your Lambda function like we did in [Module 2: Create a Lambda function](https://github.com/GivenCingco/Modulus-Python-Web-Application-/blob/main/README.md#module-2-create-a-lambda-function).
- In a new browser tab, open the [DynamoDB console].(https://us-east-1.console.aws.amazon.com/dynamodbv2/home?region=us-east-1#dashboard)






























