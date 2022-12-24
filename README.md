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


![Screenshot 2022-12-24 at 10 00 57](https://user-images.githubusercontent.com/50238769/209426847-52928698-8353-4682-8bb3-c8587012d760.png)


