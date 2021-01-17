# AWS Lambda:

- add trigger to trigger the function.
- test: imported or written code can be tested right on AWS.
- monitoring: do see couldwatch data regarding the function.
- handler: refers to index.js file and the function name it exports to trigger the function, and all other functions it possibly runs thru main function.
- environment variables: allow dev to passing in environment config variables depending on the environment the code is running in, ie, dev, production etc.
- tags: add and used in data analytics.
- execution roles: defines the permissions of the file. default is automatically passed in.
- settings: configures function timeouts, ramp up memory to use incase you have a complexed function. will cost more.

### Lambda function promise method template:

    exports.handler = (event, context, callback) => {
    // TODO implement


    // call back initiates end of the function, returning either error or data.
    callback(null, event);

};
