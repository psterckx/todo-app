# Todo App

## For the _Create a full-stack app with AWS_ workshop at CUhackit 2022

## About

This project contains a simple todo app built with [VueJS](https://vuejs.org/).

For this app to work with a backend, you'll need to provide your API's url in the `App.vue` file

The get tasks and complete/uncomplete tasks features are already built. Here are some other features that you could build!

- Create a task
- Update the name of a task
- Delete a task
- Order tasks (by name, by created date, by whether the task is complete or not)
- Better error handling with snack bars
- Dark mode

## Frontend

### Set up

```
npm install
```

### Serve locally

```
npm run serve
```

### Build

```
npm run build
```

## Backend resources

### Bucket policy for website hosting

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "Statement1",
      "Principal": "*",
      "Effect": "Allow",
      "Action": ["s3:GetObject"],
      "Resource": ["YOUR_BUCKET_ARN_HERE/*"]
    }
  ]
}
```

### Lambda function for getting tasks

```js
const aws = require("aws-sdk");
aws.config.update({ region: "us-east-1" });

const documentClient = new aws.DynamoDB.DocumentClient();

// scan is not efficient for large datasets, read the DynamoDB documentation to learn more
async function getTasks() {
  const tasks = await documentClient.scan({ TableName: "tasks" }).promise();
  return {
    statusCode: 200,
    body: JSON.stringify({ tasks: tasks.Items }),
  };
}

exports.handler = (event) => {
  return getTasks();
};
```
