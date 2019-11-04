### The Console - Your best friend
This chapter is a short but important intermezzo.
Maybe you have already encountered the console. Whenever you write code your computer does not understand it will tell you so in the console. And worse, it will also block you from running your scene! C# as a programming language is very, very picky about it’s syntax and what works and what not. “Strongly typed” is the fancy computer science term for that. C# even expects you to to care about capitalization. We as humans are prone to making mistakes and thus sooner or later you are bound to produce an error. If you haven’t, go ahead and deliberately do so. Any typo is good enough:
{{<highlight c>}}
transform.positio = transform.positio + new Vector3(1, 0, 0)* Time.deltaTime;
{{</highlight>}}
![Console Error](/img/consoleError.jpg)
As soon as you do your computer will complain. But not only will he complain, he will also try to tell you what it is he does not understand:
`Assets\Scripts\MovingAlbersVar.cs(19,19): error CS1061: 'Transform' does not contain a definition for 'positio' and no accessible extension method 'positio' accepting a first argument of type 'Transform' could be found (are you missing a using directive or an assembly reference?)`
In this case, he tells us, that he knows about Transform but has no concept of “positio”. And well, of course he doesn’t! 
He is also kind enough to also print out the line in which he has problems understanding you. So this is typically the place where you should start your process of debugging. You can even just double-click on the error message and Unity will directly take you to the line that is causing the error.
Dealing with errors can be very disheartening. But!... what you always have to remember is, that this never means, that you are bad programmer. Mistakes happen! Especially in the beginning. They will stay and that’s fine. Everyone knows this happens and that’s why every code editor will try to do it’s best to prevent you from making errors in the first place. Auto-completion for example can help to avoid errors. Any red squiggly line in the code editor is an attempt to tell you Unity will produce an Error in the code.

Apart from errors Unity also displays “Warnings” here. Warnings aren’t going to break your code immediately. This could for example happen if you use functions that are “Obsolete”. Meaning they are still here for legacy reasons, but will in later Versions of Unity be removed from the code. If you are just playing around, feel free to ignore stuff like this, but at least look into what the alternative is in the future.
Warnings can be manifold, so if you are run into one and the displayed message isn’t helpful try looking it up in your favorite search engine.

TODO Inspector Debug Mode


### The power of “Debug.Log”
Often in programming we think about what we want to achieve and yet the computer does not do what we want him to. Especially as a beginner we often assume the computer knows something it doesn’t. So we can actually ask the Computer to tell us what he thinks is going on. 
You could for example print out the value for our sinus Variable at each frame to check if it is really staying between 0 and 1.
{{<highlight c>}}
Debug.Log(sinus);
{{</highlight>}}
If you now run your code, and check the Console you should se the value printed out each Frame.
You can have as many Debug.Log Statements in your code as you want, but they will slow down the execution of your code, so once you don’t need one anymore, get rid of it. They also should not be in your code anymore, once you “ship” it.
If you have a Debug.Log statement in your code, which you don’t need right now, but think it could be useful down the line, you can also just comment it out for the moment being.
And while this is a really helpful way to get a better grasp of your code, you shouldn’t get in the habit of cluttering them all over the place in your code.


### Breakpoints
In addition to Debug.Log you can also use so called breakpoints. Breakpoints allow you to specify a line of code inside your IDE and once your program reaches that line, Unity will switch back to the IDE and you can click on all the variables and check their current values. This is a fantastic tool for debugging your code. you can even go into Playmode directly from the IDE. But it sadly is restricted to IDEs, so you will need to use Visual Studio Community oder Jetbrains Rider, while Code Editors like Visual Studio Code will not suffice.
Here is how to use them in Visual Studio Community, which ships with Unity:
Inside the Code Editor on the far left of the document window you will see grey bar. You can simply click in on that bar in front of the line you want to use as a breakpoint. At this line a red dot will appear and the line will be colored red, meaning your breakpoint is set up.
In the topbar of your IDE you will find a button called “Attach to Unity” and a drop down arrow right beneath it which will allow you to also choose “Attach to Unity and Play”. Select either one. If you opt for the first one you have to switch to Unity and enter play mode manually.
Once the light you specified is encountered Unity will switch back to your VS Community and mark the line yellow. It will also pop up a few windows on the bottom, i.e. a list of all the variables currently active and which values are assigned to them. You can fully explore the object.
Once you have found your problem you can easily press the red dot again and it will vanish, bringing everything back to normal.
ScreenShots!
Walk through line by line missing!
F10 and F11
You cant edit code while you are debugging!!!


### Still stuck?
If you are stuck, there are several places to look for help.
The first place you should always check out are the Unity Docs. You can find them at https://docs.unity3d.com. 
The Unity Documentation are really, really helpful and consists of two different parts. The first part is the manual. It consists of descriptions of all Components and Workflows in Unity as well as tutorials and Guides on some topics. It also has some great insight about optimizations for your scenes and so on. Be sure to check it out.
The other part is the Unity Scripting API. (You can switch between both in the upper right corner.)
API is short for Application programming interface and it’s the things Unity lays open for you to acces through code. Like the transform.position. So you could search for transform. The first entry will show you a list of all the things you can access on that component. That is a lot of stuff and you will never need everything. 
Now think about all other components and think about everything they might lay open. Nobody can remember everything, so it’s great that we can look this stuff up so conveniently.
If you choose on of it’s properties or functions you can get even more details and in most cases even see example code, which is really helpful!
You will always find the most recent version of the docs online, but if you happen to have a slow internet connection you could try Zeal as an offline documentation browser. I have it installed on my Laptop as a great way to search the docs when I’m on the train. You can find it at zealdocs.org.


