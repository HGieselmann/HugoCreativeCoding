# Github
### Let’s talk about Version Control
You probably noticed, or will soon, that sometimes you have an idea on how to improve your code. You reformat your code, delete some old code here some there and all is good. The next day you look at your code an realize that it was laaate last night and everything you did, was just breaking stuff. But what did you actually change last night??

For Unity you have two options about taking care of this. There is the easy and very convenient way of using Unity Collaborate. Once logged in you can easily upload your projects to Unity Collaborate and restore previous states of your project directly from Unity. In the free Personal Edition of Unity you will get 2GB of free Storage and all your projects will automatically be private. While using Unity Collaborate definitely fine, reading on, will help you to feel like a real hacker. Which is nice too! Also as we move through this book we will definetly look into getting code from Sources like Github.

So this other option is a little bit more tech-savy but will also teach you to do this independently from Unity using Git. Unity developers themselves use this to share their code with the community and have people look at examples.

Git is a Version Control Software that is freely available. Whenever you feel like you made a good step forward you can “commit” a.k.a. save your progress and if you ever need to go back to that state - you can! <br>
Now while Git locally is nice, git “Remotes” is what makes it really awesome! This allows you to, for one have  a remote backup as well as more easily collaborate with other people. And once your project grows maybe you have a team and you can all work on the same project. <br>
There are many commercial providers for remote Git-Repositories, most offer free accounts for small projects. You could look for Mircrosofts Azure Repos, GitKraken, BitBucket by Atlassian, GitLab or, as we will do Github. Github today is also owned by Microsoft. <br>
Which one you choose is totally up to you, but I will use Github through out this book, as it is what Unity Technologies is using for their public repositories.

So what exactly does Git do?
Git allows you to store stages of your project and go back in time. This is called a commit. You can also branch out. This means you maybe have the idea for a completly new UI for your game, but don’t want to break things. Then you can create a new “branch” and develop this new UI you or the rest of your team continue working on the rest of the project. Once you finished the new UI, you can make a “pull request”. This will ask the owner of the repository (this may, or may not be you yourself) to merge the changes to your project. Before you merge the code git will make sure both branches are still compatible to one another and then merge them together.<br>
All of this can be done using the GUIs provided by your Remote Repository Provider or using the commandline. We will go the commandline way, as it is universal.


### Basic Git Usage
Before we can get into commandline magic we need to install git on our computer. Check out this post by derhuerst on Github Gist, to find out how:[Link](https://gist.github.com/derhuerst/1b15ff4652a867391f03)<br>
Next go ahead and create an Account at Github.com. Once your Account is created and you again open up github.com You will see a Green button with a little Book in it saying “New”. Click it. Now enter a name for your repository or and the optional description. With a free account you will not be able to choose wether the Repository will be public or private, but you can and absolutly should add a .gitignore file. Click the “Add .gitignore” Button and search for Unity and add it. <br>
This file will make sure Git will include files that are unnecessary to track. Finally click “Create Repository”.

Now you a you have an empty repository in the cloud. Everything else we will handle from the Commandline. Go ahead and open up a “Terminal” Window on the Mac or Commandline or Powershell if you are on Windows. There are a few short Commands you will need to learn to navigate the commandline. <br>
`ls` short for list, will print out all the files and folders on the directory you are in. <br>
`cd` short for change directory, will allow you to change the directory. If you want to go deeper one level just put the name of the folder you want to enter, or the path of serveral folders you want to go. <br>
To go up a level just do a `cd ..` Or type the path from the beginning like `cd C:\`. <br>
Now use these commands to navigate to your Unity Project Folder.

Once you are there type `git status`. This will print out the current status of the Folder. In  our case it should tell you, that it is not a repository yet. So we need to initialize it: <br>
`git init` will do this for us. Form now on it will try to track changes to our Folder. But this is just locally, so we still need to connect it to our Github.com Repository! <br>
`git remote add origin PathYoYourGitRepo.git` <br>
You can just copy and paste the path from Your browser and add the `.git` at the end. <br>
If this goes without failure, our Project Folder and our Online Repository are linked together, but both are in different states! So while Git will not let us push to the cloud we still can pull from it. And that’s a good thing. This way we will receive the `.gitignore` file Github created for us. So, do a <br>
`git pull origin master` <br>
Git will now download the state of the project from the Cloud for us. Now we can savely add files to our repository, because git will igonre all the files and folders defined in the `.gitignore`-File. <br>
Everything we did just now, is a thing, that we only need to do once for every project. You will get used to it over time, but definetly feel free to use the TL;DR at the bottom to sneek at the code when doing this for other projects.

The following steps you will do quite often, as they are the three Key steps to track your project. It’s adding files, commiting the changes and pushing them to the cloud. <br>
`git add -- all` will add all the files to our repository. From now on their history and changed will be tracked by git. <br>
`git commit -m “I changed the following stuff: this is a comment` <br>
You might think, the `-m` with comment is not important. Git will not commit without a comment! <br>
Then do a push! <br>
`git push origin master` <br>
This will trigger an upload Github. Now all your important files will be tracked and saved in the cloud! Commit early and often!

###TL;DR <br>
How to setup your project with Github: <br>
* Create Repo with `Unity.gitignore` on the Github Website <br>
* In the Commandpromt/Terminal navigate to your Unity Project Folder <br>
* Code to execute one by one: <br>

	Git init <br>
	Git remote add origin LinkToGithubRepo.git <br>
	Git pull origin master <br>
	Git add -A <br>
	Git commit -m “Comment” <br>
	Git push origin master <br>


