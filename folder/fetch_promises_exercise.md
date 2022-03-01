[HOME](/README.md)

# AJAX with fetch and DOM manipulation

1. **clone the repo from GitHub**

    https://github.com/dat3startcode/SimpleWebpackBabelForPlainJS.git

## ES6 classes and Single Page Applications - No fetch()

2. **[Watch this video before the exercise!](https://www.youtube.com/watch?v=Kc0a43cY-tk)**

* This exercise assumes you have installed nodejs, and a JavaScript editor like vs-code
* Clone the project referred to above, and navigate into the project root folder:
* In this folder type npm install to fetch all dependencies (as had it been a Maven project)
* Type npm run build (yes before deployment this project has to be built)
* Take a quick look inside the generated build folder, and look no further in this folder for the rest of the exercise
* Now open the project in your favorite IDE (with vs code just (in the terminal) type code .)
* Back in the terminal type npm start.
* Now arrange your windows so you can see both your editor window (with the code) and the browser with the simple menu.
* Keep your windows arranged like this for the rest of the exercise.

3. **Render all jokes**

    Take a look inside ``index.html`` in the public folder, and locate the part marked for exercise-1. Here you should see an ul-tag with id=jokes.

    In ``index.js``, get all jokes from the ``jokeFacade`` and create, using the arrays map-method, list-items for all jokes and place them in ul.

    **Hint:** The video referred to above shows how to do that.

4. **Finding individual jokes**

    In the ``index.html`` file, below the ul-tag we used above, add an input field, a button with the text get joke, and a p-tag to hold the joke you want to find.
    
    Investigate the start code and implement functionality (in index.js) to find a joke, given it’s id.

5. **Adding new Jokes**
    In the ``index.html`` file, below what you did in the previous step, add the necessary changes to add new jokes to the internal joke-facade.

***

## Small application to display a quote.

Your task is to fetch random Chuck Norris jokes and show them like this:

 <figure>
    <img src ="../images/chucky.png"
         alt ="chuck norris jokes"
         width =""
         height ="">
    <figcaption><em>Chuck Norris Jokes</em></figcaption>
</figure>

1. Locate the section in index.html reserved for exercise-2 and add a button + an empty p-tag (which will hold the quote we fetch), both with id’s so they are easy to “find”
2. Add an event listener to the button’s click event and pass a callback that will update the p-tag in the index.html with a new quote fetched from the API given below
3. Initially, fetch the quote from a remote API: https://api.chucknorris.io/jokes/random
4. Use fetch() to get the quote.
5. Use developer-tools in your browser and the network tab to monitor the AJAX-request.
**Important:**  Explain why, what you did above, is possible, when we know the Same Origin Policy governs where AJAX-requests can go.
6. Change the functionality to get a new quote every minute. (Hint: use setInterval())

***

## Ajax with a full REST CRUD Endpoint and Error-handling

Creating Single Page Applications often requires the development of both a front-end (the SPA) and a backend (often REST_JSON based). For this reason, it would be convenient if we had a way to quickly set up a mock-backend to use while developing our frontend.
Several such mock-backends exist, with json-server as one of the most popular. It allows us to set up a backend in less than a minute which can use data in a JSON-file as it’s “database”. Unfortunately, it does not provide errors as JSON, so for this exercise, we will use a modified version, twisted for our needs this week.

1. Clone this  json server https://github.com/Cphdat3sem2018f/code_jsonserver_with_errors
The users.json file in the project root folder will act as the persistence media for your database, and will change when you start to add/edit/delete via the REST-API provided by the server:

2. [Watch this video before you start!](https://www.youtube.com/watch?v=KUgU5npkv2k)

3. Inside the project type:
    - ``npm install``
    - ``npm start`` (see the readme file for alternative ways to start.  You will eventually need them all)

    Now you have a test server running with a full CRUD REST API, available via http://localhost:3333/api/users
    Leave this terminal open for the rest of the exercise, and verify that the server is running

4. Enter this URL in your browser: http://localhost:3333 and read the instructions.

5. Test the servers GET-methods in a browser, using these URLs

        GET: http://localhost:3333/api/users/
        GET: http://localhost:3333/api/users/110
        GET: http://localhost:3333/api/users/1111111111  (to see an error-response)

6. Add a ``rest.http`` file to your project. Create a POST request to http://localhost:3333/api/users/

    with following headers:

        Content-Type : application/json
        Accept: application/json
    
    and following body:

        {
        "age": 23,
        "name": "Peter Pan",
        "gender": "male",
        "email": "peters@pan.com"
        }

    Verify, via your browser that the new user has been added with an id.

7. Try each of the following scenarios:
    - Same user as above, but age = 2. Observe the response (and status code)
    - Same user as above, but name=”ib” Observe the response (and status code)
    - Same user as above, but gender =”mand” Observe the response (and status code)
    - Same user as above, but an illegal email.Observe the response (and status code)

## Test the PUT method

1. Make a PUT request up against PUT: http://localhost:3333/api/users/**ID**

    with following headers:

        Content-Type : application/json
        Accept: application/json


    Set the body as the user returned from your first POST request, but change the name to something else.

    Verify, via your browser that the user has been changed.

***

## Implement a Single Page Application that uses the API investigated above

Since this is (probably) your first true Single Page Application, and since both the front- and backend-server involves a lot of new “magic”, like clone xxx, node, npm install, npm start etc. It can be hard to “see” the overall architecture of what you are building. This, however, is important, so use the figure below to get an idea about the “architecture” of what you will be building. Right now your backend should be running in a separate terminal (the API: /api/users) and you are about to start on the front-end (the SPA).

 <figure>
    <img src ="../images/single.png"
         alt ="spa"
         width =""
         height ="">
    <figcaption><em>Single Page Application</em></figcaption>
</figure>

1. [Watch this video for an easy start](https://www.youtube.com/watch?v=l5ahJkMXYGE)

2. Continue with the Client Side Project used from the very beginning of these exercises or clone a new version for this project.

3. Start the project, and locate the grid for exercise-3, this is where you have to add the following 5 functionalities:
    1. Show all users (in a table)
    2. Show a single user, given an ID
    3. Add a new User
    4. Edit an existing user
    5. Delete an existing user

## Error Handling

If not already done, provide the fetch examples above with sufficient error handling so that:

- A request for a non-existing user, must render the error message provided by the server.
- Breaking one or more of the rules for new users, while submitting a new user, must render the error message provided by the server.