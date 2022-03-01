[HOME](/README.md)

# Promises and Fetch Guidelines

Without having to install external  API’s, there are only two ways to make AJAX-requests in a browser:

- The old, and original way, using the  XMLHttpRequest method (works in all browsers).
- Using Fetch which is included in all newer browsers.

The biggest difference between the two is  that fetch is using promises, which is the modern and recommended way, to handle asynchronicity in JavaScript.

Fetch is a bit tricky to use, in cases where error-response for 4xx and 5xx errors are supplied as a JSON-response, but the following will suggest a possible solution, and we recommend fetch as the API to use.

## Promises

We will not dig in deep to the promise-API this semester, but as a minimum, you should know that a JavaScript Promise object represents the eventual completion (or failure) of an asynchronous operation and its resulting value. 

Think of a Promise as the JavaScript counterpart to Java’s Futures.
For this semester you need to know the fundamentals of promises since fetch is using, and returns, promises.
