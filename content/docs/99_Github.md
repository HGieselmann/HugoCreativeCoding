Title: MasterS3  
Author:   


Let’s talk about Version Control.
You probably noticed, or will soon, that sometimes you have an idea on how to improve your code. You reformat your code, delete some old code here some there and all is good. The next day you look at your code an realize that it was laaate last night and everything you did, was just breaking stuff. But what did you actually change last night??

For Unity you have two options about taking care of this. There is the easy and very convenient way of using Unity Collaborate. Once logged in you can easily upload your projects to Unity Collaborate and restore previous states of your project directly from Unity. In the free Personal Edition of Unity you will get 2GB of free Storage and all your projects will automatically be private. While using Unity Collaborate definitely fine, reading on, will help you to feel like a real hacker. Which is nice too! Also as we move through this book we will definetly look into getting code from Sources like Github.

So this other option is a little bit more tech-savy but will also teach you to do this independently from Unity using Git. Unity developers themselves use this to share their code with the community and have people look at examples.

Git is a Version Control Software that is freely available. Whenever you feel like you made a good step forward you can “commit” a.k.a. save your progress and if you ever need to go back to that state - you can!
Now while Git locally is nice, git “Remotes” is what makes it really awesome! This allows you to, for one have  a remote backup as well as more easily collaborate with other people. And once your project grows maybe you have a team and you can all work on the same project.
There are many commercial providers for remote Git-Repositories, most offer free accounts for small projects. You could look for Mircrosofts Azure Repos, GitKraken, BitBucket by Atlassian, GitLab or, as we will do Github. Github today is also owned by Microsoft.
Which one you choose is totally up to you, but I will use Github through out this book, as it is what Unity Technologies is using for their public repositories.

So what exactly does Git do?
Git allows you to store stages of your project and go back in time. This is called a commit. You can also branch out. This means you maybe have the idea for a completly new UI for your game, but don’t want to break things. Then you can create a new “branch” and develop this new UI you or the rest of your team continue working on the rest of the project. Once you finished the new UI, you can make a “pull request”. This will ask the owner of the repository (this may, or may not be you yourself) to merge the changes to your project. Before you merge the code git will make sure both branches are still compatible to one another and then merge them together.
All of this can be done using the GUIs provided by your Remote Repository Provider or using the commandline. We will go the commandline way, as it is universal.

Before we can get into commandline magic we need to install git on our computer. Check out this post by derhuerst on Github Gist, to find out how: https://gist.github.com/derhuerst/1b15ff4652a867391f03 S
Next go ahead and create an Account at Github.com. Once your Account is created and you again open up github.com You will see a Green button with a little Book in it saying “New”. Click it. Now enter a name for your repository or and the optional description. With a free account you will not be able to choose wether the Repository will be public or private, but you can and absolutly should add a .gitignore file. Click the “Add .gitignore” Button and search for Unity and add it.
This file will make sure Git will include files that are unnecessary to track. Finally click “Create Repository”.

//TODO FROM HERE
Now everything else will happen on the commandline. Open up a terminal, commandline or powershell Window. Then navigate to your Unity Project Folder.
TODO Add Commandline navigation
Then type in “git status” to get the current state of your repository. It should tell you, that this is not a Git repository.
Then type “git init” to initialize your project folder as a Git Repository.
“Git remote add origin Linktoyourgitrepository.git”
“Git pull origin master”
“Git add -A”
Let it do it’s thing.
“Git commit -m “fancy comment”
“Git push origin master”

