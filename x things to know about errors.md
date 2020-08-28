__X things to know about errors in Javascript__

Errors and error handling is such a big deal. And although this article encapsulate the most importants things you need to know about errors and how to handle them. The knowledge should create the awareness in quickly identifying errors and knowing exactly where to look on one hand, and preventive measure on the other hand. 

__Types of error__

Officially the type of errors as classified by Javascript include the following- EvalError, InterenalError, RangeError, ReferenceError, SyntaxError, TypeError, URIError. 
(https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Error)

However, they are more error types we have to mitigate as developers and classifying them into this category makes more sense to me and it comprehensive. 


- runtime error / execution error / exceptions
(causes app to crash if...)
could be various types. Eg. a typeError when the wrong input is provided. A wrong time error is essentially a valid a javascript code with form of error
e.g Invalid input, failed connection, system out of memory, exceeded callstack(v)

- parse error / syntax error
Is an invalid javascript code error. Typically this type of errors are caught by the by the IDE and usally syntax errors. 

- logical error. when a  programming is not working as intended. This type of errors are best caught by writing the necessary automated test

- program error - when property is undefined. For this it common to use if statement around the undefined variable. 

- fatal error (v)

- uncaught error/exception

- library/tooling errors- Eg. linting errors, commit errors, typescript errors

- API and network errors. (the 4xx and 5xx) 

- Validation errors

- routing errors

__Methodology__
- try... catch... finally 
- .then()... .catch()


__Thinking__

In handling errors one ask the following-  Should I use throw, return or console.error? Keeping in the mind the customer experience and not being a lazy developer who wants to console all errors. 

__Handling Errors__

1. Display a message to the user
2. Log error to the server
3. Log to console if ENV is in development
4. Have a standardize error reporting that would be used in handling errors. 
5. In some case like network error, simply use a retry (axios-retry is a great library for that)
6. The type of error should determine the type of response. Generic response are bad for errors that can be identify. 
7. Having human readable error message
8. Think of internationalization as part of your error handling design
9. Think of async validation in handling validation error
10. Redirect the user in some cases.

__Others__

- throw will by default terminate the execution of the program and log to console in the absence of a catch block. If a catch block exist; then the error will be handle as specified.

- return will terminate the program with no error log

- remember the try...catch can be used outside async functions and method eg. async await

- try ... catch only handles runtime errors

- In handling error, the defaults in the default error handlers like catch will do just fine; however, custom errors will have to thrown for Example
```js
throw new SyntaxError("Incorrect input")
// SyntaxError is the name of the error and the string the () is the message
```

- The difference between error and exception.
An error is an instance of the Error class, it can be passed as a parameter to another function or it can be thrown. The error becomes an exception when it’s thrown.

- Nodejs usually handles error with a callback pattern e.g
```js
fs.readFile("./config.txt", function(err, data) {
  if (err) {
    console.error("There was an error reading the file!", err)
    return
  }
  // Handle the data
  console.log(data)
})
```

- There are different ways to handle errors. However, that should be a very important part of your thinking as a programmer. 

- uncaught exception is used to refer to errors which have been handled in our code. This will by default be logged to browser console. And this type of error is best caught on the windows object to prevent the app from crashing

- InternalError is an error on the Js engine caused by computational issues such as indefinite loops, recursion and all 

- example of how to handle unhandled exception
```js
window.onerror = function (message, file, line, col, error) {
   alert("Error occurred: " + error.message);
   return false;
};
window.addEventListener("error", function (e) {
   alert("Error occurred: " + e.error.message);
   return false;
})
```
- On the server in nodeJs / express, error are handle sometimes via a reroute

- To enhance the user experience, it also worth while to determine what error are shown to the user and those that handle quietly

Q. why must the Error be handled with a class 

```js
class MyError extends Error {
  constructor(message) {
    super(message);
    this.name = 'MyError';
  }
}
vs
function MyError(message) {
    this.name = 'MyError';
    this.message = message;
    this.stack = (new Error()).stack;
}
MyError.prototype = new Error;  // <-- remove this if you do not 
                                //     want MyError to be instanceof Error
```