# Serveless

## History

- Data centre
- IAAS
- PAAS
- Containers
- Serverless

# Lambda

AWS lambda is a compute service where you can upload your code and create a lambda funciton. AWS Lambda takes care of provision and managing the servers that you use to run the code. You don have to worry about operating systems, patching, scaling, etc. You can use Lamdba in the following ways:
- As an event-driven compute Service where AWS Lambda runs your code in response to events. These events could be changes to data in an Amanzon S3 bucket or an Amazon DynamoDB table.
- As a compute service to run your code in response to HTTP requests using Amazon API gateway or API calls made using AWS SDKs

## Price

- **Number of requests**: first 1 million requests are free, after $0.20 per 1 million requests thereafter.
- **Duration**: calculated from the time your code begins executing until it returns or otherwise terminates, rounded up to the nearest 100ms. The price depends on the amount of memory you allocate to your function. You are charged $0.00001667 for every GB-second used.

## Advantags

- No servers
- Continuous Scaling (out, not up)
- Super cheap!

## Version Controll

When you use versioning in AWS Lambda, you can publish one or more versions of your Lambda funcitions. As a result, you can work with different variations of your Lambda function in your development workflow, sush as development, beta and production.
Each Lambda function version has a unique Amazon Resource Name (ARN). After you publick a version, it is immutable (that is it cannot be changed).
AWS Lambda maintains yourlatest fuction code in the $LATEST version. When you update your function code, AWS Lambda replaces the code in the $LATEST version of Lambda function.

### Qualified/Unqualified ARN

- You can refer to this function using its Amazon Resource Name (ARN). There are two ARNs associated with this initial version
- **Qualified ARN** the function ARN with the version suffix (arn:aws:lambda:aws-region:acct-id:function:helloword:$LATEST)
- **Unqualified ARN** the function ARN without the version suffix (arn:aws:lambda:aws-region:acct-id:function:helloword)

### Alias

After initially creating a Lambda Function (the $LATEST version), you can publish a version 1 of it. By creating an alias named PROD that points to version 1, you can now use the PROD alias to invoke version 1 of the Lambda function.
Now you can update the code (the $LATEST version) with all of your improvements and then publish another stable and improved version (version 2). You can promote version 2 to production by remapping the PROD alis so that it point to version 2. If you find something wrong, you can easily roll back the production version to version 1 by remapping the PROD alias so that it points to version 1.

- Can have multiple version of lambda functions
- Latest version will use $latest
- Qualified version will use $latest, unqualified will not have it
- Versions are immutable (Cannot be changed)
- Can split traffic using aliases to different versions
- Cannot slip traffic with $latest, instead create an alias to latest


## Exam tips

- Lambda funcitons are independent, 1 event = 1 function
- Lambda functions can trigger other lambda functions, 1 event can trigger X other functions.
- AWS X-ray allows you to debug what is happening
- Lambda can do things globally, you can use it to back up S3 buckets to other buckets, etc.
- Know your triggers

# API Gateway

Is a fully managed service that makes it easy for developers to publish, maintain, monitor and secure APIs at any scale. With a few clicks in the AWS Management Console, you can create an API that acts as a "front door" for applications to access data, business logic or functionality from your back-end services, such as applications running on Amazon Elastic Compute Cloud (Amazon EC2), code running on AWS or any web application

### Type of APIS

- REST APIs (REpresentation State Transfer)
- SOAP APIs (Simple Object Access Protocol)

## What can API Gateway Do?

- Expose HTTPS endpoints to define a RESTful API
- Serverless-ly connect to services like Lambda & Dynamo DB
- Send each API endpoint to a different target
- Run efficiently with low cost
- Scale effortlessly
- Track and control usage by API key
- throttle requests to prevent attacks
- Connect to CloudWatch to log all requests for monitoring
- Maintain multiple versions of your API

## Configure of API Gateway

- Define an API (container)
- Define resources and nested resources (URL paths)
- For each resource:
  - Select suported HTTP methos (verbs)
  - Set security
  - Choose target (such as EC@, Lambda, DynamoDB, etc)
  - Set request and response transformations
- Deploy API to a Stage
  - Uses API Gateway domain, by default
  - Can use custom domain
  - Now supports AWS Certificate Manager: free SSL/TLS certs.

# API Caching

You can enable API caching in Amazon API Gateway to cache your endpoints's response. With caching, you can reduce the number of call made to your endpoint and also improve the latency of the requests to your API. When you enable caching for a stage, API Gateway caches responses from your endpoint for a specified time-to-live (TTL) period, in seconds. API Gateway then responsds to the request by looking up the endpoint reponse from the cache instead of making a request to your endpoint.

# Same Oring Policy

In computing, the same-origin policy is an important concept in the web application security model. Under the policy, a web browser permits scrips contained in a first web page to access data in a second web page, but only both web pages have the same origin.
This is done to prevent Cross-Site Scripting (XSS) attacks, enforced by web browsers and ignored by tools like PostMan and curl.
**Cross-Origin Resource Sharing (CORS)** is one way the server at the other end (not the client code in the browser) is a mechanism that allows restricted resources (e.g. fonts) on a web page to be requested from another domain outside the domain from whith the first resource was served.

- Browser makes an HTTP OPTINS call for a URL (OPTIONS is an HTTP method like GET, PUT and POST)
- Server returns a response that says: "these other domains are approved to GET this URL"
- Error: "Origin policy cannot be read at the remote resource?" you need to enable CORS on API Gateway

## Exam Tips

- Remenber what API Gateway is at high level
- API Gateway has caching capabilities to increase performance
- API Gateway is low cost and scales automatically
- You can throttle API Gateway to prevent attacks
- You can log results to CloudWatch
- If you are using Javascript/AJAX that uses multiple domains with API Gateway, ensure that you have enabled CORS on API Gateway
- CORS is enforced by the client