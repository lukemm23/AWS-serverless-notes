# Endpoint testing templates:

### get template: (extra params provided for GET type 'all')

    let xhr = new XMLHttpRequest();
        xhr.open('GET', 'https://ixg2jkk4gh.execute-api.us-east-2.amazonaws.com/dev/compare-yourself/all'),
        xhr.onreadystatechange = function(event){
            console.log(event.target.response);
        }
        xhr.setRequestHeader('content-type', 'application/json');
        xhr.send();

### post template: (data body provided inside xhr.send())

    let xhr = new XMLHttpRequest();
        xhr.open('POST', 'https://ixg2jkk4gh.execute-api.us-east-2.amazonaws.com/dev/compare-yourself'),
        xhr.onreadystatechange = function(event){
            console.log(event.target.response);
        }
        xhr.setRequestHeader('content-type', 'application/json');
        xhr.send(JSON.stringify({age:26, height:71, income:2100}));

### delete template: (data body provided inside xhr.send())

    let xhr = new XMLHttpRequest();
        xhr.open('DELETE', 'https://ixg2jkk4gh.execute-api.us-east-2.amazonaws.com/dev/compare-yourself'),
        xhr.onreadystatechange = function(event){
            console.log(event.target.response);
        }
        xhr.setRequestHeader('content-type', 'application/json');
        xhr.send(JSON.stringify({age:26, height:71, income:2100}));
