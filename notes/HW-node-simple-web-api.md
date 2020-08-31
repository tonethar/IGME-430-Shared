# HW - Node Simple Web API


## I. Overview

- We are going to create a simple [*Web API*](https://en.wikipedia.org/wiki/Web_API) using node and npm
- Because this is a very simple app, we are going to do so without using any node packages such as [Express](https://www.npmjs.com/package/express)
- We are going to deploy the code for our API to the ["platform as service"](https://www.heroku.com/platform) provider [Heroku](https://www.heroku.com/#) using Git & Github
- This web service will serve up a random joke in [JSON](https://www.json.org/json-en.html) format
- Below are screenshots of the landing page for the service, the `/stale-joke` and `/random-joke` endpoints, and a client web app that uses the web service

<hr>

**The landing page**

![screenshot](_images/_simple-node-web-api/ss-1.png)

<hr>

**`/stale-joke`**

![screenshot](_images/_simple-node-web-api/ss-2.png)

<hr>

**`/random-joke`**

![screenshot](_images/_simple-node-web-api/ss-3.png)

<hr>

**A client web app that uses the random-joke [endpoint](https://stackoverflow.com/questions/2122604/what-is-an-endpoint)**

- the code for this client provided at the end of this tutorial

![screenshot](_images/_simple-node-web-api/ss-4.png)

<hr>

## II. Getting ready

1) You need a console app to type commands into:
    - On Mac OS you can use the built in *Terminal* app
    - On Windows you can use one of these:
      - [Windows Terminal](https://www.microsoft.com/en-us/p/windows-terminal/9n0dx20hk701)
      - GitBash (this also installs git) - https://www.stanleyulili.com/git/how-to-install-git-bash-on-windows/
      - Powershell - https://docs.microsoft.com/en-us/powershell/scripting/install/installing-powershell
    - You should also know some basic Unix commands such as `cd`, `ls` and `pwd` - [Unix Cheatsheet](http://www.rain.org/~mkummel/unix.html)
    
2) You must have node & npm installed - see the install instructions here --> https://docs.npmjs.com/downloading-and-installing-node-js-and-npm

3) If you are going to deploy this to app to Heroku you will need:
    - A Github account (free!) - https://education.github.com/pack
    - Git - https://git-scm.com/book/en/v2/Getting-Started-Installing-Git
    - A Heroku account (free!) - https://signup.heroku.com

<hr>

## III. Get started - creating and cloning a GitHub repository

- So that we can deploy this app (our web API) to the web using Heroku, we will need to set up a GitHub repository for the app. This is because Heroku uses GitHub to upload the app's files (as opposed to using an FTP client if we were working with a web server like Apache)
- If you do not intend to deploy this app to the web and will instead just run it locally, then you can skip the steps below. Instead, just create a folder on your desktop named **joke-service**

1) Login to your GitHub account and create a new repository named **joke-service** - you don't need to add a README or anything - just keep it empty

2) Copy the *clone URL*

<hr>

![screenshot](_images/_simple-node-web-api/ss-5.png)

<hr>

3) Open your console app (Terminal, GitBash, et al.)

4) *Change directory* to whatever folder on your computer that you want to do work in:
    - you can accomplish this by typing `cd`, then a space, and then dragging the folder into the console window, which should copy the file path to that folder into the console window. The type enter.
    - On Unix/Linix machines like Mac OS, or in GitBash, you should go ahead and verify that your [*current working directory*](https://en.wikipedia.org/wiki/Working_directory) is your chosen folder by typing `pwd` (*print working directory*)
    
5) Type `git clone <url>` (replace `<url>` with the clone URL of your repository)

6) Type `ls` to verify that you have downloaded your (empty) repository

<hr>

![screenshot](_images/_simple-node-web-api/ss-6.png)

<hr>

## IV. Create a package.json file
  
1) Type `cd joke-service` to make **joke-service** your current working directory. Then type `pwd` to verify that you were successful.

<hr>

![screenshot](_images/_simple-node-web-api/ss-7.png)

<hr>

2) Type `npm init -y` to create a **package.json** file with the default values - https://docs.npmjs.com/cli/init

    - it will look something like this:
    
```js
{
  "name": "joke-service",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "repository": {
    "type": "git",
    "url": "git+https://github.com/tonethar/joke-service.git"
  },
  "keywords": [],
  "author": "",
  "license": "ISC",
  "bugs": {
    "url": "https://github.com/tonethar/joke-service/issues"
  },
  "homepage": "https://github.com/tonethar/joke-service#readme"
}
```

- Go ahead and add values for `"author"` and `"keywords"` if you want

<hr>

## V. Create index.js

1) Inside of **joke-service**, create a folder named **src**

2) Inside of **src**, create a file named **index.js**

3) Add this line of code to **index.js**

```js

console.log("Server starting up ...");

```

4) Test your code by typing `node ./src/index.js` into the console (assuming that your current working directory is **joke-service**):
  - you should see `Server starting up ...` logged to the console


<hr>

![screenshot](_images/_simple-node-web-api/ss-8.png)

<hr>

## VI. Update package.json

1) The first thing we are going to add to **package.json** is a `"start"` key (which goes under the `"scripts"` key) 
    - the `"start"` key will have a value of `"node ./src/index.js"`
    - the the `"scripts"` key of your **package.json** file should now look this:
    
```json
"scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "start": "node ./src/index.js"
  },
```

2) On the command line, type `npm start` - which is short for `npm run start` - this will run the command you just added to the **package.json** file (i.e) the value of the `"start"` key. This does the same thing we did in Part V. above, but with less typing and remembering!

<hr>

![screenshot](_images/_simple-node-web-api/ss-9.png)

<hr>

3) Now we are going to install ONE npm package - just one external dependency - the nodemon project - this is going to be a *development dependency* that will make our lives easier:
    - you can read about it here: https://www.npmjs.com/package/nodemon
    - what nodemon will do for us will be to automatically restart our app any time we make changes to our files - this will end up saving us a lot of time over the long haul of writing and debugging an app
  
4) To install nodemon for just this app type `npm install --save-dev nodemon`

<hr>

![screenshot](_images/_simple-node-web-api/ss-10.png)

<hr>

5) The `--save-dev nodemon` flag will add a `"devDependencies"` key to **package.json** - which looks something like this (your version number may vary):

```js
"devDependencies": {
    "nodemon": "^2.0.4"
  }
```

6) To use the monitoring capabilities of nodemon, we just need to add this to the `"scripts"` key of **package.json**:
    - `"nodemon": "nodemon --watch ./src ./src/index.js"`
    - The above command will "watch" the contents of the `src` folder for changes, and when it sees any it will restart the server by running the script at "./src/index.js"
    - the the "scripts" key of your package.json file should now look this:
    
```js
"scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "start": "node ./src/index.js",
    "nodemon": "nodemon --watch ./src ./src/index.js"
 }
```
    
7) Now test nodemon by typing `npm run nodemon` in the console, and then make a small change to **index.js**:
    - you should see the server restart and the change reflected in the console:

<hr>

![screenshot](_images/_simple-node-web-api/ss-11.png)

<hr>

## VII. Serve up the landing page

- Now that we have the project setup, let's finally write some code to serve up our web API's default "landing page" that documents the API endpoints
- Recall that we are not going to use the Express package to do this - why not?
  - This a pretty simple app, so we don't need any of the functionality that Express provides
  - By instead using the built-in capabilities of Node's **http** module, we can avoid a 500+ kByte download and (more importantly) 51 dependencies - https://arve0.github.io/npm-download-size/#express


1) Type the following into **index.js**

<hr>

![screenshot](_images/_simple-node-web-api/ss-12.png)

<hr>

- the first line of code imports the built-in **http** module and aliases it to a `http` variable in our program - you can read about **import** and the **http** module here: 
    - https://nodejs.org/api/modules.html#modules_require_id
    - https://nodejs.org/api/http.html#http_class_http_serverresponse
- the second line of code sets up a *port* (which you can read about here - [Port_(computer_networking)](https://en.wikipedia.org/wiki/Port_(computer_networking)) - which will be 3000 when we test locally. One of the other values (`process.env.PORT` & `process.env.NODE_PORT`) will be used as a port value when this app runs in the cloud on Heroku
- the third line of code is the HTML string for our landing page. More commonly this HTML be stored in a separate file or template and then loaded in by our JavaScript, but we're trying to keep this example simple:
  - note that the entire string is an ES6 [Template Literal](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Template_literals) and enclosed in backticks (the key near your escape key) NOT single-quotes

2) Note that nodemon should be automatically rebooting the server everytime you save any changes to **index.js** - before you move on - be sure that there are no syntax errors and that the successfully code runs

<hr>

![screenshot](_images/_simple-node-web-api/ss-13.png)

<hr>

3) Here's our joke data - it's an array of [object literals](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Object_initializer) - each of which has a `"q"` and an `"a"` key. Here it is for your copy & paste pleasure:

```js
const jokes = [
	{"q" : "Why did the chicken cross the road?", "a" : "To get to the other side!"},
	{"q" : "What do you call a very small valentine?","a":"A valen-tiny!"},
	{"q" : "What did the dog say when he rubbed his tail on the sandpaper?","a":"Ruff, Ruff!"},
	{"q" : "Why don't sharks like to eat clowns?","a":"Because they taste funny!"},
	{"q" : "What did the boy cat say to the girl cat?","a":"You're Purr-fect!"},
	{"q" : "What is a frog's favorite outdoor sport?","a":"Fly Fishing!"}
];
```

4)

<hr>

![screenshot](_images/_simple-node-web-api/ss-14.png)

<hr>

- ddd

<hr>

![screenshot](_images/_simple-node-web-api/ss-15.png)

<hr>
