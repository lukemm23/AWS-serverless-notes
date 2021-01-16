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

    create method:
    	- integration type:
    	    1. Using a lambda function
    	    2. Regular HTTP method
    	    3. Call another AWS service
    	    4. Mock data
    	- use lambda proxy integration: passing data into the lambda function. and give the enpoint method permission to run specified lambda function.
    	- refer to lambda function by typing function name into the input.
        - once lambda function is setup, click test to test connection, if successful, you should get the callback message or error back.

    deploy API:
    - select deploy API
        1. choose new stage
        2. fill out stage name, stage description, and deployment description.
    - once deployed, the deployment is listed inside stages.
