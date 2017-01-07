# Create Hubot Project
Ok, let's get started with ChatOps by creating a Hubot Project.

### Introducing Hubot
We are going to use Hubot for our platform. (https://hubot.github.com/)

Let's take a few minutes to review the documentation to get started... https://hubot.github.com/docs/

### Pre-Requisites:  
You will need node.js and npm installed to continue.

```
# Confirm node.js version
node -v
v5.12.0

# Confirm npm version
npm -v
3.8.6
```

### STEP 1: Yeoman and Hubot Generator
Let's install yeoman and a generator we'll use to create our hubot project.
```
npm install -g yo generator-hubot

```

### STEP 2: Create New Github Repository
Let's go ahead create our Git Repository on GitHub
- Repository Name: hubot
- Public: Yes
- Do Not Initialize README
- Add Write Permissions to for our Engineers

### STEP 3: Clone New Git Repo
Let's clone the new repo to our local workstation
```
cd /Users/<username>/Github/copyleft-cloud
git clone git@github.com:Copyleft-Cloud/hubot.git
git clone git@github.com:Copyleft-Cloud/hubot.git
   Cloning into 'hubot'...
   warning: You appear to have cloned an empty repository.
```

### STEP 4: Generate the Hubot Project
Let's generate our hubot project using the yeoman generator
Since, we going to be using Slack, we selec the Slack Adapter upfront.
Have fun and pick a good name and personality for your hubot... we selected the name Burton after Jack Burton from the Cult Classic Big Trouble in Little China.

```
cd /Users/<username>/Github/copyleft-cloud/hubot
yo hubot --adapter=Slack

? Owner Copyleft.io <cloud@copyleft.io>
? Bot name burton
? Description A simple helpful robot for your Company
   create bin/hubot
   create bin/hubot.cmd
   create Procfile
   create README.md
   create external-scripts.json
   create hubot-scripts.json
   create .gitignore
   create package.json
   create scripts/example.coffee
   create .editorconfig
```

### STEP 5: Review the Project
Let's review our Project Directory
```
hubot $ ls -al
total 64
drwxr-xr-x   13 brian.hooper  1446486574   442 Jan  7 02:16 .
drwxr-xr-x    5 brian.hooper  1446486574   170 Jan  7 02:07 ..
-rw-r--r--    1 brian.hooper  1446486574   197 Oct 22  2014 .editorconfig
drwxr-xr-x    9 brian.hooper  1446486574   306 Jan  7 02:07 .git
-rw-r--r--    1 brian.hooper  1446486574    39 Dec 19  2014 .gitignore
-rw-r--r--    1 brian.hooper  1446486574    24 Jan  7 02:16 Procfile
-rw-r--r--    1 brian.hooper  1446486574  7823 Jan  7 02:16 README.md
drwxr-xr-x    4 brian.hooper  1446486574   136 Jan  7 02:16 bin
-rw-r--r--    1 brian.hooper  1446486574   213 Jan  7 02:16 external-scripts.json
-rw-r--r--    1 brian.hooper  1446486574     2 Jan  7 02:16 hubot-scripts.json
drwxr-xr-x  175 brian.hooper  1446486574  5950 Jan  7 02:16 node_modules
-rw-r--r--    1 brian.hooper  1446486574   649 Jan  7 02:16 package.json
drwxr-xr-x    3 brian.hooper  1446486574   102 Jan  7 02:16 scripts
```

### STEP 6: Test from the Shell Adapter
Let's test a sample command from /scripts/example.coffee using the Shell Adapter
```
# Uncomment & Save
robot.hear /badger/i, (res) ->
    res.send "Badgers? BADGERS? WE DON'T NEED NO STINKIN BADGERS"
```

Run Hubot from the Shell
```
./bin/hubot

burton> badger
burton> Badgers? BADGERS? WE DON'T NEED NO STINKIN BADGERS
```

Success... we now have a working Hubot that we can test with at the Shell.

### STEP 7: Push an Initial Commit to Github
Following our successful test, let's push our initial commit to our Git Repository on Github.
```
git status
git add .
git commit -m "Initial Commmit"
git push -u origin master
git status

```

## Summary
- We've Installed yeoman and the hubot generator
- We've Created a New Hubot Project
- We've Tested our first script/command via the Shell Adapter
- We've Pushed our initial commit to Github

## Next Steps
- First, let's deploy a DigitalOcean Droplet to host our hubot
- Second, let's set up a continuous delivery pipeline via Travis-CI for our Hubot
