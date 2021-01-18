# API gateway:

### Side nav Overview:

    - Create API: create new path, takes in path type such as REST, HTTP etc
    - Create resource: creating a new path
    - Create Method: creates a single GET, POST, PUT, DELETE route inside a path
    - Import API: importing
    - Deploy API: takes a snap shot of current API to be used or tested on
    - Stages: tracks deployed versions of the API
    - Authorizer: setting up authentication for the API, using ie. Incognito etc.
    - Model: defines shape of data to work with inside API, uses JSON schema language
    - Documentations: used to doc info about API incase you are using in a team, or leave the API open to public.
    - Binary support: sending files along with requests.
    - Dashboard: shows stats of the API, usage data, errors thrown, a high level view.

### End point method info overview: can require authorization with API key

    * input:
        - method request: info about client request to API, configure query params (info on query params like id), request headers(status, or search term), request body(incoming data), sdk settings
        - integration request: info about API request to data source, transforming incoming data and perform business logic with ie. Lambda functions. To send to data source.

    * output:
        - integration response: getting back data from data source, extract/transform data and perform business Logic.
        - method response: sending response back to client. Header, res.body, params.

### Creating API

    1. proxy resource check box: using one resource as the sole resource of whole API to a project.
    2. API gateway CORS check box: cross origin resource sharing, a security feature for info sharing. By sending a header to client to allow sharing. Options for handling external requests. When enabled header options will have extra header options inside integration response.

### Create method:

    	- integration type:
    	    1. Using a lambda function
    	    2. Regular HTTP method
    	    3. Call another AWS service
    	    4. Mock data
    	- use lambda proxy integration: passing data into the lambda function. and give the enpoint method permission to run specified lambda function.
    	- refer to lambda function by typing function name into the input.
        - once lambda function is setup, click test to test connection, if successful, you should get the callback message or error back.

### Deploy API:

    - select deploy API
        1. choose new stage
        2. fill out stage name, stage description, and deployment description.
    - once deployed, the deployment is listed inside stages.

### Data Control and validation: (defining / manipulating data)

    3 ways of data control
        1. using model to define data shape at method request
        2. using integration request and response and define body mapping templates
        3. write logic in code inside lambda function.

    1. from Integration Request
    - select integration request: (when "Use Lambda Proxy" is checked)
        1. check Use Lambda Proxy integration to pass complete data not just request body to the function
        2. integration response will be grayed out, and CORS header will not be found. to fix it, lambda function callback() will need to return (null, {headers:{'Control-Access-Allow-Origin':'*'}})
        to send over CORS permission.
        3. see "Lambda Logs" accessing data/event
    - select integration request: (when "Use Lambda Proxy" is not checked)
        1. use mapping template (when no template is selected, all of data body will be forwarded).
        2. check when there are no templates defined and add a template.
        3. name "application/json"
        4. select "method request passthrough" or refer to body mapping language to custom write template.
        5. ie.
            test data: {"personData":{"name":"luke"}},
            mapping template: {"name" : $input.json('$.personData.name')},
            will return: "luke",
            cloudwatch log will return: { name: 'luke' }.

    2. from Integration Response
    - select integration response:
        1. you can forward body mapping from integration request to response.
        2. ie.
            test data: {"personData":{"name":"luke"}},
            request mapping template: {"name" : $input.json('$.personData.name')},
            response mapping template: {"your-name" : $input.json('$'),
            will return: {"your-name": "luke"},
            cloudwatch log will return: { "your-name": 'luke' }.

    3. using model
    select model:
        1. create new model, and use JSON schema language to define model.
        2. go to method request > request validator > check validate body.
        3. go to method request > request body > register model.
        4. you can also import model inside integrations request and response mapping template.

### Lambda Logs:

    - all event logs are inside cloudwatch > log groups > select API. this is very beneficial when needing to check console logs for data.

### creating method with variable path: (using path parameters)

    1. method 1
        - create new resources name 'all' and 'single' off of existing resources.

    2. method 2
        - creating new resource name 'type', and resource path {type} as a variable.
        - create one method off of resource and take a path parameter as variable.
        - address type directed if/else statement to perform the right query.
        - go to integration request and setup body mapping template to take a type property to lambda function. ie.
            {"type":"$input.params('type')"}
        - test by passing in path {type}.

### method response model:

    - should always return data array with empty object, this can be accomplished with model.
    - create new model > name model > ie. use the same model except change type to array and then set items objects type to object and move properties model inside items object.

    {
        "$schema": "http://json-schema.org/draft-04/schema#",
        "title": "CompareData",
        "type": "array",
        "items": {
            "type": "object",
            "properties": {
                "age": {"type": "integer"},
                "height": {"type": "integer"},
                "income": {"type": "integer"}
                }
        },
        "required": ["age", "height", "income"]
    }

    - then go back to resources > click on the end point > method response > response header > and change models to new model.
