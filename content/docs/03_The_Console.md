Title: Master  
Author:   


### The Console - Your best friend
This chapter is a short but important intermezzo.
Maybe you have already encountered the console. Whenever you write code your computer does not understand it will tell you so in the console. And worse, it will also block you from running your code! As we are Coding in C#  your computer will be very, very picky about the code you write. So if you haven’t already fabricated an error. Go ahead and do so. Any typo is good enough.

	transform.positio = transform.positio + new Vector3(1, 0, 0)* Time.deltaTime;


But not only will he complain, he will also try to tell you what it is he does not understand:
`Assets\Scripts\MovingAlbersVar.cs(19,19): error CS1061: 'Transform' does not contain a definition for 'positio' and no accessible extension method 'positio' accepting a first argument of type 'Transform' could be found (are you missing a using directive or an assembly reference?)`
In this case, he tells us, taht he knows about Transform but has no concept of “positio”. And well, of course he doesn’t.
He also prints out the line in which he has problems understanding you, this is really helpful for debugging.
What you always have to remember is, that this never means, taht you are bad programmer. Mistakes happen. Especially in the beginning. But they will stay and that’s okay. That’s the reason why IDEs and CodeEditors try to check everything before you even try to compile your code.
So now that we have established that the console is our friend and not our enemy, let’s take a look at some nice additional features it has to help us when we are stuck.


### The power of Debug.Log
Often in programming we think about what we want to achieve and yet the computer does not do what we want him to. Especially as a beginner we often assume the computer knows something it doesn’t. So we can actually ask the Computer to tell us what he thinks is going on. 
You could for example print out the value for our sinus Variable at each frame to check if it is reallystaying between 0 and 1.
`Debug.Log(sinus);`
If you now run your code, and check the Console you should se the value printed out each Frame.
You can have as many Debug.Log Statements in your code as you want, but they will slow down the execution of your code, so once you don’t need one anymore, get rid of it. 
If you consider using it latyer, you can just comment it out.




### Working with the Docs
- another important part of debugging and advanding your code is the Unity docs
- https://docs.unity3d.com
- The docs consists of two parts - the manual and the scripting API
-The Manual describes how things work and also contains tutorials
- It is great place to start looking into new things or getting a deeper understanding ogf things you are working on
- You can also switch to the scripting API
- Whenever you come across the letters “API” it’s about programming
- Application programming interface
- Major social media I.e. also have APIs
- This is where you can find all the commands Unity exposes for scripting
- most of them contain example Code you can check out
- If you are stuck this can also be a wonderful place for inspiration, as maybe the function you are searching for, does not exists, but something else equally useful
-If you are slow internet Connection there are offline Documentaion browsers
- Zeal (zealdocs.org)