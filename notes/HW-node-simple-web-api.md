# HW - Node Simple Web API


# I. Overview

- We are going to create a simple [*Web API*](https://en.wikipedia.org/wiki/Web_API) using node and npm
- We are going to deploy this server to the ["platform as service"](https://www.heroku.com/platform) provider [Heroku](https://www.heroku.com/#) using Git & Github
- This web service will serve up a random joke in JSON format
- Below are screenshots of the landing page for the service, the `/stale-joke` and `/random-joke` endpoints, and a client web app that uses the web service

**The landing page**

![screenshot](_images/_simple-node-web-api/ss-1.jpg)

**`/stale-joke`**

![screenshot](_images/_simple-node-web-api/ss-2.jpg)

**`/random-joke`**

![screenshot](_images/_simple-node-web-api/ss-3.jpg)

**A client web app that uses the random-jokeservice**

- the code for this client provided at the end of this tutorial

![screenshot](_images/_simple-node-web-api/ss-4.jpg)

<hr>

# II. Getting ready

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

# III. Get started - creating and cloning a GitHub repository

- So that we can deploy this app (our web API) to the web using Heroku, we will need to set up a GitHub repository for the app. This is because Heroku uses GitHub to upload the app's files (as opposed to using an FTP client if we were working with a web server like Apache)
- If you do not intend to deploy this app to the web and will instead just run it locally, then you can skip the steps below. Instead, just create a folder on your desktop named **joke-service**

1) Login to your GitHub account and create a new empty repository named **joke-service**

2) Copy the clone url

![screenshot](_images/_simple-node-web-api/ss-5.jpg)

3) Open your console app (Terminal, GitBash, et al.)

4) *Change directory* to whatever folder you want to do work in:
    - you can accomplish this by typing `cd`, then a space, and then dragging the folder into the console window, which should copy the file path to that folder into the console window. The type enter.
    - On Unix/Linix machines like Mac OS, or in GitBash, you should go ahead and verify that your [*current working directory*](https://en.wikipedia.org/wiki/Working_directory) is your chosen folder by typing `pwd` (*print working directory*)
    
5) Type `git clone <url>` (replace `<url>` with the clone url of you repository)

<hr>

# IV. Create a package.json file
  
1) Type `cd joke-service` to make joke-service your current working directory 

2) Type `npm init -y` to create a **package.json file for this project - https://docs.npmjs.com/cli/init

    - it will look something like this:
    
```js

```