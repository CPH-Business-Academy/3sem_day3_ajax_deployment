[HOME](/README.md)

# Error Handling with fetch

A problem, which has annoyed many developers is that fetch only rejects a promise when “a network error is encountered, although this usually means permissions issues or similar.”
When a promise is rejected we can “catch” it as sketched below (using arrow notation for simplicity)

    fetch('https://swapi.co/api/people/999999999999')
    .then(res=> res.json())
    .then(data => console.log(data.name))
    .catch(err =>console.log("UPPS"));

This request returns a JSON response like this `{"detail": "Not found"}` and the status code 404. But as explained above, this http-error is not considered an error by fetch, so the example above, will not “catch” the error.

In order to handle this error (and HTTP-errors in general), and also get the error-response, we have to hook into the first then-method and check the status code.  If we want to “catch” the error, in a way, with access to the json-error, it can then be done like sketched below:

    fetch('https://swapi.co/api/people/999999999999')
    .then(res=> {
    if(!res.ok){ //OK is false for statuscodes >= 400
        return Promise.reject({status: res.status, fullError: res.json() })
    }
    return res.json();
    })
    .then(data => console.log(data.name))
    .catch(err =>{
        if(err.status){
        err.fullError.then(e=> console.log(e.detail))
        }
        else{ console.log("Network error"); }
    })

If you like this strategy (i.e. you cannot come up with something better ;-) you can create a helper function and use it for ALL your fetch-request (assuming the backend supply errors as json)

    function handleHttpErrors(res){
    if(!res.ok){
    return Promise.reject({status: res.status, fullError: res.json() })
    }
    return res.json();
    }

***

    fetch('https://swapi.co/api/people/999999999999')
    .then(handleHttpErrors)
    .then(data => console.log(data.name))
    .catch(err =>{
        if(err.status){
        err.fullError.then(e=> console.log(e.msg))
        }
        else{console.log("Network error"); }
    });
