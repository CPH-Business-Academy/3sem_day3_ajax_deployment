[HOME](/README.md)

# Fetch, with POST, PUT and DELETE

For requests other than GET,  you need to provide fetch with an object containing the options for the request you plan to do. As an example, this is how you could make a POST request:

        let options = {
        method: "POST",
        headers: {
        'Accept': 'application/json',
        'Content-Type': 'application/json'
        },
        body: JSON.stringify({
            age: 34,
            name: "lis Benson",
            gender: "female",
            email: "lis@lis.com"
        })
        }
        fetch("http://localhost:3000/users",options);

Replace method in options above,  with the actual request-method you need (PUT, DELETE). For more info read here. Please observe, that what you include for the request are (obviously) similar to how you would make the request using Postman or a http file in vscode or Intellij;

        // Example POST method implementation:
        async function postData(url = '', data = {}) {
        // Default options are marked with *
        const response = await fetch(url, {
            method: 'POST', // *GET, POST, PUT, DELETE, etc.
            mode: 'cors', // no-cors, *cors, same-origin
            cache: 'no-cache', // *default, no-cache, reload, force-cache, only-if-cached
            credentials: 'same-origin', // include, *same-origin, omit
            headers: {
            'Content-Type': 'application/json'
            // 'Content-Type': 'application/x-www-form-urlencoded',
            },
            redirect: 'follow', // manual, *follow, error
            referrerPolicy: 'no-referrer', // no-referrer, *no-referrer-when-downgrade, origin, origin-when-cross-origin, same-origin, strict-origin, strict-origin-when-cross-origin, unsafe-url
            body: JSON.stringify(data) // body data type must match "Content-Type" header
        });
        return response.json(); // parses JSON response into native JavaScript objects
        }

        postData('https://example.com/answer', { answer: 42 })
        .then(data => {
            console.log(data); // JSON data parsed by `data.json()` call
        });