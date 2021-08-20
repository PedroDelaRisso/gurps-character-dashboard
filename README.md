<h1 align="center"> GURPS Character Dashboard </h1>

<h4 align="center"> 
	🚧  Work in progress  🚧
</h4>

<p align="center">
 <a href="#objective">Objective</a> •
 <a href="#technologies">Technologies</a> •
 <a href="#requirements">Requirements</a> •
 <a href="#running">Running the app</a> •
 <a href="#author">Author</a>
</p>

### [Objective and about the project](#objective)
Build an app that facilitates rolls of any attribute, skill or damage for any character sheet in GURPS 4e. One that is easy to use and setup. Currently it is easy to use, but not as easy to setup, and it is far from ready.
I intend to add as many rules and features from GURPS 4e into this dashboard.

This project is being done as a means to study VueJS further (as I need this to do my current job). As of now (20/Aug/2021) the backend of this app is a "fake" rest API using a json server. For the near future, if everything goes ok, I want to change the backend to .NET 5.

Have a look at what I have so far!

### [Technologies](#technologies)
* [VueJS 3](https://v3.vuejs.org/)
* [NodeJS](https://nodejs.org/)
* [GitHub Desktop](https://desktop.github.com)
* [Git](https://git-scm.com)
* [Visual Studio Code](https://code.visualstudio.com)

### [Requirements](#requirements)
Before starting, you'll need [NodeJS](https://nodejs.org/) and [Git](https://git-scm.com) installed on your machine.
And a code editor, I use [Visual Studio Code](https://code.visualstudio.com).

### [Running the app](#running)
### • First, installation
Create a folder for the app's installation. Inside the folder you created, right click and select ``Git bash here``. And then run this command to clone this repository:
```bash
git clone https://github.com/PedroDelaRisso/gurps-character-dashboard.git
```
### • Then, running the thing
Open a command terminal on the repository folder, you can do this using VSCode's keyboard shortcut ``Ctrl+'``. Execute the batch file ``Install.bat`` and then the other batch file ``Start.bat`` or run these commands:
```bash

cd client
# Install the packages needed to run and build the app:
npm install 
# Wait for everything to be installed and then run:
npm run serve
```
As for the backend, open a new terminal, as you need both executing at the same time, and run these commands:
```bash
cd client

npm run backend
```

If everything goes fine, you can access the app inside your browser, by navigating to [localhost:8080](http://localhost:8080). You may face problems as some browsers deny direct connection to the localhost. If you use any Chromium based browser, as Chrome or Vivaldi, you can paste this in the address bar: ``chrome://flags/#allow-insecure-localhost``. The first option in the list should read as "Allow invalid certificates for resources loaded from localhost". Set it to enabled and now you're all set to run this app!


### [Author](#author)
---

<a href="https://github.com/pedrodelavechiasoitic//">
 <img style="border-radius: 50%;" src="https://cdn.discordapp.com/attachments/861972486362890270/865216130548367391/eu.jpg" width="100px;"/>
 <br />
 <sub><b>Pedro Delavechia Risso</b></sub></a> <a href="https://github.com/PedroDelaRisso//"
