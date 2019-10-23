## Lessons learned from Promise Bot / Improvements for the future

### Better logging. 
* Lets create a shell of an application with a logger setup with different logging
* And then dig into what the app is going to be

### Deployment strategy
* Serverless? If so, lets have a serverless app up and running as a simple hello world app before adding functionality
* With server? Need better user control. 
  * How do we deploy code again?
  * Maybe create a deployment user that can do a git pull and own the files on the application

### Promises and Awaits
* Awaits are just better promises
* Lets use awaits as much as we can unless we're exmlicitly trying to benefit from parallel performance of a promise, then structure

### Handling Promise Rejections
* EVERY promise must have a then and catch block
* EVERY await must have a catch
* Pay particular attention to Db functions, there is an assumption they always work, so we don't need to error handle
* Not every error needs to be caught, logged and ignored
  * Inside every catch block, think about what it means for that function to be in error
  * Can we simply catch it, log it, and keep going?
  * Or will the change be breaking for app functionality, in which case we need to catch the error and then throw it
  * If we do throw the error, every function that calls that function much also decide what to do with thrown error
  * For the almost every case, we'll need to bubble that throw error all the way up to the top layer (bot or UI)
  * Let the user know what the error is
* Basically the goal should be -> No unhandled promise exceptions in the logs
