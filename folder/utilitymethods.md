[HOME](/README.md)

# Fetch utility methods

This page contains some small utility functions to make your life with fetch more “fun”
Utility method for POST, PUT and DELETE requests
Remember, for requests other than GET, you need to provide an options object to fetch.

This small method (refer to the spec, for additional properties you can set):

        function makeOptions(method, body) {
        var opts =  {
        method: method,
        headers: {
            "Content-type": "application/json",
            "Accept": "application/json"
        }
        }
        if(body){
        opts.body = JSON.stringify(body);
        }
        return opts;
        }

***

You can make the POST request from our previous example as simple as this:

        const data = {age: 34,name: "lis Benson", gender: "female",email: "lis@lis.com"};
        const options = makeOptions("POST",data);
        fetch("http://localhost:3000/users",options);

***

Utility Method to handle http-errors with fetch
This is the same as was introduced earlier in the section “Error handling with fetch”

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
