# CORS setup:

### Testing: (CORS errors won't show up on console, therefore it needs to be tested from external server.)

    - use codepend.io to run code: (mimic-ing a external request)

    let xhr = new XMLHttpRequest();
        xhr.open('POST', 'https://ixg2jkk4gh.execute-api.us-east-2.amazonaws.com/dev/compare-yourself'),
        xhr.onreadystatechange = function(event){
            console.log(event.target.response);
        }
        xhr.send();

        1. if content-type is not set add:
        ie: xhr.setRequestHeader('content-type', 'application/json');

        2. if data body is incorrect try:
        ie: xhr.send(JSON.stringify({age:36, height:70, income:3100}));

    - go into resources > endpoint > method response: add new header name: Access-Control-Allow-Origin
    - go into resources > endpoint > integration response: set value for newly created header: '*' (allow access from all external servers and origins.)
    - re-deploy to the specified stage and overwrite to old stage.
    - run test again to get mesage response successfully.

    - once setup, go to resource and click enable CORS to setup same config to all methods.
