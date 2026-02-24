# AWS LAMBDA

`AWS Lambda`
- WIth Lambda AWS manages all the server, we just need to upload our source code
- It's compute service that lets us run code without having to provision or manage servers. 
- We copy our code to AWS, and AWS will manage the underlyne infrastucrture like spinning the necessary **EC2 Instances**. This is none as Serverless offering.
- Lambdais AWS's Serverless offering i.e
  - AWS manages the **server maintainance**, Scaling, Capacity **Provisioning**, and **logging**
  - When we get more traffic its gonna spin up more instances automatically and copy the source code automatically to each Instance


## USE CASES
- `File Processing` E.g: We've an application that allows user to upload images to an S3 bucket, and we want to have these images resize for our Web Application, We can have a `Lambda Functions` that triggers the `S3 buckets` anytime a file is being uploaded, grab the image, resize it and send it to another S3 bucket

- its Great for Web API

## 3 Main Component of Lambda 

1. `Lambda Function`: This just a regular function code we want to run
 
```js
export.handler = async function (event, context){
    console.log("Lambda function run");
    return;
}
```

2. `Trigger`: This is something that happens and triggers Lamnda function should run. Example could be a file that get uploaded to S3, A request to an API Gateway etc

3. `Event`: This is the information about what trigger took place.

# Benefit of Lambda
- No servers to manage from users
- No need for an Infrastructure Team to Manage the server
- No need for Patching / upgrading
- faster development
- Auto scale to handle traffic spikes
- Pay for what you use
  - Pay per Invocation i.e whenever the Lambda function was called
  - No extra cost during low traffic

# Downsides of Lambda
- No local state, therefore, we need a seperate database to store data that needs to persist e.g `Dynamo DB`
- Limited Execution Duration i.e Function can run at most for 15mins
- Not good for long running tasks
- Cold Starts: This occur due to the time it takes to initialize and load the function


# Lambda Pricing

- We get charged for number of times the Functions ran
- we get charged How long Funtion ran for 
- We get charged how much memory / CPU did it require