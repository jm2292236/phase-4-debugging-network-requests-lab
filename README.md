# Putting it All Together: Client-Server Communication

## Learning Goals

- Understand how to communicate between client and server using fetch, and how
  the server will process the request based on the URL, HTTP verb, and request
  body
- Debug common problems that occur as part of the request-response cycle

## Introduction

Just like the last lesson, we've got code for a React frontend and Rails API
backend set up. This time though, it's up to you to use your debugging skills to
find and fix the errors!

To get the backend set up, run:

```console
$ bundle install
$ rails db:migrate db:seed
$ rails s
```

Then, in a new terminal, run the frontend:

```console
$ npm install --prefix client
$ npm start --prefix client
```

Confirm both applications are up and running by visiting
[`localhost:4000`](http://localhost:4000) and viewing the list of toys in your
React application.

## Deliverables

In this application, we have the following features:

- Display a list of all the toys
- Add a new toy when the toy form is submitted
- Update the number of likes for a toy
- Donate a toy to Goodwill (and delete it from our database)

The code is in place for all these features on our frontend, but there are some
problems with our API! We're able to display all the toys, but the other three
features are broken.

Use your debugging tools to find and fix these issues.

There are no tests for this lesson, so you'll need to do your debugging in the
browser and using the Rails server logs and `byebug`.

**Note**: You shouldn't need to modify any of the React code to get the
application working. You should only need to change the code for the Rails API.

As you work on debugging these issues, use the space in this README file to take
notes about your debugging process. Being a strong debugger is all about
developing a process, and it's helpful to document your steps as part of
developing your own process.

## Your Notes Here

- Add a new toy when the toy form is submitted

    - How I debugged:
        - I tried to add a new toy using the frontend app and saw a response from the server with code 500 at the handleSubmit function.
        - Checked routes.rb and found the route actions for **index**, **create** and **update** are already in place.
        - I used rails console and tried to add a new toy, it worked well.
        - Checked the backend server logs and found the error was: 
            - **NameError (uninitialized constant ToysController::Toys):**
            - **app/controllers/toys_controller.rb:10:in `create'**
            - which is caused because in the create action the name of the Toy class is misspelled as "Toys".
        - Corrected the misspelling and now the user is able to add new toys. **Task finished!**
    

- Update the number of likes for a toy

    - How I debugged:
        - Tried to add a like to a toy in the frontend app and got this error displaying on the console:
            - **Uncaught (in promise) SyntaxError: Unexpected end of JSON input**
        - Already know that this kind of error is caused because the backend server is not rendering json data back
          but the frontend app is expecting it.
        - Modified the controller's create action to render json.
        - Tried again to add a like to toys and it worked as expected.
    

- Donate a toy to Goodwill (and delete it from our database)

    - How I debugged:

