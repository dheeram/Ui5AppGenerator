# AppGen

The AppGenerator is used to create Ui5 Apps. It contains a template app that is copied and the files that contain the project name get changed. A simple proxy (http capable) is used to connect to the odata services of the gateway. The template app is customizable but the files need to be included in the code. It works a bit like the ui5 tooling but is not limited to one app at the time and brings a few other features. The current functions include adding services, views and dialogs to existing apps, creating new apps, building the app and deploying apps to the gateway. Ui5 tooling is installed and used to build the apps. Thanks to the guys over there, they do wonderful work! If you programm Ui5 apps yourself you will understand the code of this app as well, just take a look :)

Is is based on node.js and express. Customise as much as you need to make it work for you. I want to make the apps work offline as well. To achieve self-sufficient apps I have to use the ui5 toolinge serve. You could klick on an app, the tooling will kick in, and host it parallel to the AppGenerator.

Most likly the best thing would be to pack my management tools into a middleware extension, but I work alone and don't have to knowledge to do that. If someone want to help me with that please let me know, I would love to do that!


# Installation

For the installation only node.js is required and the cli has to be available. The following packages are in use.

 - UI5: npm install --global @ui5/cli
	 - Used for build process
 - Git: npm install --global git
     - Codemanagement. Used in combination with a local git installation for the login
 - NPX: npm install --global npx
     - Deploys the apps to the gateway

Dont forget the **npm install** after downloading the AppGen.

Relocate the **start.bat** to the main Folder.
Fill the .env File:

    GW_USR=
    GW_PWD=
    GW_URL= (No Port / https)
    HOST=
    WORKDIR=

The "work-dir" is pointing at the folder where the start.bat / AppGen is saved. For example "\\Documents\\Git\\", the user dependet part is solved via the node module OS and its *homedir* funktion (see Index.js app.zWorkDir).

# Folder Structure
-----------------Location of start.bat....
The setup I intended for this is to have the *start.bat* in the same folder as all the apps (including AppGen):
 - ...User/Documents/
  - Git/
   - AppGen
    - webapp/
    - package.json
    - [...]
   - App1
   - App2
   - [...]
   - start.bat

The content of the start.bat is the following:

    cd C:\nodejs
    start  "" http://localhost:443/AppGen/webapp/index.html
    node ./AppGen/index.js

If you start it with the batch file, your standard browser opens and the node.js webserver will run local on port 443. This way you are able to open all the apps you have in that folder (Git) at the same time, hop between them and so on. Depending on your network settings you can open the apps with the ip of the pc, the port and your login from any pc. If you would realy want you could host it on a server, I would not do that because then you would loose the easy flexibility.

# Git behavior

This is not a fully build git helper. It only covers the basic function. Those are mostly automated.
If you open the git helper after creating a new app you have to provide the url to the repository.
You need to have an accessible connection to your git server. I use a tfs in combination with a local git client that is providing the login credentials.
The url to your repository is saved in you project in the file *zProjInfo.json* and the variable *gitInitialized* is set to true. When you entered a correct url and press init git the app will get staged, commited and pushed (origin/master).
After the initial git push you can enter the commit messages in the git panel (same button). The commit and push button stages all changes, commits them and uses the git status to check for pull/merge information. A git pull is executed before the push. If something isn't working the git status shows underneath the message field.

# Planned features
- mockgen (work in progress)
- editable namespace (currently fix in template app)
- translate the readme to english (fehlgeschlagen)

- better placeholder using (done)
- Ui5core.js local (scrapped)