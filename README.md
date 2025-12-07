# Fetch-Data-with-AWS-Lambda
 I will diving into the data tier, which is all about how you store and manage the data relevant to your application.


# Fetch Data with AWS Lambda



**Author:** Darryl Brown  
**Email:** darrylbrown1991@gmail.com

---

## Fetch Data with AWS Lambda

![Image](http://learn.nextwork.org/sincere_vermilion_playful_beaver/uploads/aws-compute-lambda_p9thryj2)

---

## Introducing Today's Project!

In this project, I will diving into the data tier, which is all about how you store and manage the data relevant to your application. I'm doing this project to demonstrate the 3rd layer of a Three-Tier architecture. I will demonstrate how to use a serverless AWS Lambda function to retrieve data from a DynamoDB table. This is perfect for roles such as Backend Developers, Cloud Engineers, and some cases DevOps Engineers where it is a key responsibility to create scalable cloud solutions that handle large amounts of data efficiently.

### Tools and concepts

Services I used were DynamoDB, JSON, AWS Lambda, IAM, Data, CloudWatch. Key concepts I included Lambda functions, Data retrieval, Lambda function test, DynamoDB table, three-tier architecture. 

### Project reflection

This project took me approximately 35 minutes. The most challenging part was create my own JSON permission policies. It was most rewarding to create the connection between AWS Lambda and Dynamo DB. 

I chose to do this project today to demonstrate the third layer of the Three-Tier architecture. 

---

## Project Setup

To set up my project, I created a database using AWS DynamoDB. The partition key is the heart of how DynamoDB organizes data. Which means it's how DynamoDB spreads out data across different servers for quick access and efficient querying.

In my DynamoDB table, I added a JSON code defines a new item for my UserData table. DynamoDB is schemaless, which means you can add attributes as you need, and every item in your database can have a different set of attributes. This flexibility is one of the key benefits of using a NoSQL database like DynamoDB.

![Image](http://learn.nextwork.org/sincere_vermilion_playful_beaver/uploads/aws-compute-lambda_a112c3d5)

### AWS Lambda

AWS Lambda is a service that lets me run code without needing to manage any computers/servers, Lambda will manage them for me. Lambda runs my code only when I need it to (so I'm not paying for any idle time). It also scales automatically, from a few requests per day to thousands per second. All I need to do is supply my code in one of the languages that Lambda supports.

---

## AWS Lambda Function

My Lambda function has an execution role, which is an IAM role for my Lambda function. It defines what the function is allowed to do, like accessing other AWS services like DynamoDB. By default, the role grants AWS creates a role for Lambda with basic permissions for writing logs to CloudWatch. 

My Lambda function first half of the code uses the AWS SDK for JavaScript to interact with DynamoDB. It takes a userId as input, grabs the corresponding data from the UserData table, and returns it to me. The second half of the code handles potential errors during the database operation, so I get a tailored error message that tells me what went wrong.

The code uses AWS SDK, which is AWS Software Development Kit, a set of tools that let developers build apps that interact with AWS. My code uses SDK to use pre-written functions for communicating with DynamoDB and getting data from a table. Without the SDK, I'd have to manually write the code to interact with AWS, which would be much more complex and error prone.

![Image](http://learn.nextwork.org/sincere_vermilion_playful_beaver/uploads/aws-compute-lambda_a1b2c3d5)

---

## Function Testing

To test whether my Lambda function works, I went to the test tab in my Lambda function and wrote in JSON then selected test. If the test is successful, I'd see a green tab saying " executing function: succeeded" with a CloudWatch link

The test displayed a 'success' because the message simply means the function itself could run but the function's response was actually a 400 because we haven't given it explicit permission to access my DynamoDB table.

![Image](http://learn.nextwork.org/sincere_vermilion_playful_beaver/uploads/aws-compute-lambda_u1v2w3x4)

---

## Function Permissions

To resolve the Access Denied error I can add a permission policy that gives me the permissions I'm lacking. 

There were a few DynamoDB permission policies I could choose from, but I didn't pick "AWSLambdaDynamoDBExecutionRole" and "AWSLambdaInvocation-DynamoDB"  because ExecutionRole gives Lambda function the permissions to see a DynamoDB stream. LambdaInvocation is used to automatically trigger Lambda functions in response to events captured in DynamoDB stream. 

I also didn't choose AmazonDynamoDBFullAccess, my  Lambda function only needs to read data, I don't need this level of access. Granting this permission when I don't need it can make my resources less secure. AmazonDynamoDBReadOnlyAccess was the right choice because it has GetItem in the policy

![Image](http://learn.nextwork.org/sincere_vermilion_playful_beaver/uploads/aws-compute-lambda_3ethryj2)

---

## Final Testing and Reflection

To validate my new permission settings, I re-ran my Lambda function test. The results were successful because it shows the user data I added in my DynamoDB table with no error message. 

Web apps are a popular use case of using Lambda and DynamoDB. Lambda can be a serverless backend for web apps, grabbing data from DynamoDB when a user logs in or interacts with my app. For example, I could use Lambda to help social media apps fetch user profiles or automatically retrieve all content like videos or images linked with a profile. Lambda can help news sites or blogs fetch articles based on user queries.

![Image](http://learn.nextwork.org/sincere_vermilion_playful_beaver/uploads/aws-compute-lambda_p9thryj2)

---

## Enahancing Security

For my project extension, I challenged myself to to create an inline policy. This will allows for more granular control. In this case, I only want my Lambda function to access the UserData table, so an inline policy is more secure.

To create the permission policy, I used create inline policy and edited in JSON to my preferences. 

When updating a Lambda function's permission policies, you could risk running into error. I validated that my Lambda function still works by running another test on my Lambda function's.

![Image](http://learn.nextwork.org/sincere_vermilion_playful_beaver/uploads/aws-compute-lambda_1qthryj2)

---

---
