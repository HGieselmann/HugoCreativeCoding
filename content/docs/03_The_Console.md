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




### Still stuck?
If you are stuck, there are several places to look for help.
The first place you should always check out are the Unity Docs. You can find them at https://docs.unity3d.com. 
The Unity Documentation are really, really helpful and consists of two different parts. The first part is the manual. It consists of descriptions of all Components and Workflows in Unity as well as tutorials and Guides on some topics. It also has some great insight about optimizations for your scenes and so on. Be sure to check it out.
The other part is the Unity Scripting API. (You can switch between both in the upper right corner.)
API is short for Application programming interface and it’s the things Unity lays open for you to acces through code. Like the transform.position. So you could search for transform. The first entry will show you a list of all the things you can access on that component. That is a lot of stuff and you will never need everything. 
Now think about all other components and think about everything they might lay open. Nobody can remember everything, so it’s great that we can look this stuff up so conveniently.
If you choose on of it’s properties or functions you can get even more details and in most cases even see example code, which is really helpful!
You will always find the most recent version of the docs online, but if you happen to have a slow internet connection you could try Zeal as an offline documentation browser. I have it installed on my Laptop as a great way to search the docs when I’m on the train. You can find it at zealdocs.org.
