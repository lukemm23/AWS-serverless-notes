# AWS Lambda:

- add trigger to trigger the function.
- test: imported or written code can be tested right on AWS.
- monitoring: do see couldwatch data regarding the function.
- handler: refers to index.js file and the function name it exports to trigger the function, and all other functions it possibly runs thru main function.
- environment variables: allow dev to passing in environment config variables depending on the environment the code is running in, ie, dev, production etc.
- tags: add and used in data analytics.
- execution roles: defines the permissions of the file. default is automatically passed in.
- settings: configures function timeouts, ramp up memory to use incase you have a complexed function. will cost more.
- assign a fitting role, and check if existing role is there when creating a function that is not the first function.

- go to API gateway and configure connection to lambda function
  1. choose the correct region
  2. function should populate at lambda function input.

### Lambda function promise method template:

    exports.handler = (event, context, callback) => {
    // TODO implement


    // call back initiates end of the function, returning either error or data.
    callback(null, event);
    };

### lambda function example for POST new object into dynamoDB tables. (refer to AWS sdk dynamoDB docs for more examples)

    const AWS = require('aws-sdk');
    const dynamodb = new AWS.DynamoDB({region: 'us-east-2', apiVersion: '2012-08-10'});

    exports.handler = (event, context, callback) => {
        console.log(event)
        const params = {
            Item: {
                "UserId": {
                    S: "user_" + Math.random()
                },
                "age": {
                    N: event.age
                },
                "height": {
                    N: event.height
                },
                "income": {
                    N: event.income
                }
            },
            TableName: "compare-yourself"
        };
        dynamodb.putItem(params, function(err, data) {
            if (err) {
                console.log(err);
                callback(err);
            } else {
                console.log(data);
                callback(null, data);
            }
        });
    };

### lambda function example for GET new object into dynamoDB tables. (refer to AWS sdk dynamoDB docs for more examples)

### lambda function example for DELETE new object into dynamoDB tables. (refer to AWS sdk dynamoDB docs for more examples)

    const AWS = require('aws-sdk');
    const dynamodb = new AWS.DynamoDB({region: 'us-east-2', apiVersion: '2012-08-10'});

    exports.handler = (event, context, callback) => {
        const params = {
            Key:{
                "UserId":{
                    S: "user_0.3657827152096518"
                }
            },
            TableName: "compare-yourself"
        };

        dynamodb.deleteItem(params, function(err, data){
            if(err){
                console.log(err)
                callback(err);
            }else{
                console.log(data);
                callback(null, data);
            }
        })
    };
