### Designing Code
Before we dive deeper into considerations about design, let’s take a very short break and discuss designing code. As with many things in design, there are often many, many ways to solve one and the same problem. You soon will, or already have seen, me writing code that you would have approached differently. And it is definitely possible that your solution is better. (And please let me know if you think I do some really stupid stuff!!LinkToContactSheet) But maybe it’s just a different approach to the problem. Five programmers will solve the same problem in 5 different ways and that’s fine.
But there are can also be differences in the effort put in to solving the problem. Yes you can solve many problems naming your variables `x1` to `xn`. But will you remeber what `x1` and `x2` were meant to be, when you look at your code one month later? You probably can’t. So you will have to read through that again and try to figure out, what they were meant to be in the first place. 
 So this chapter is devoted to some basic conventions about writing beautiful code. We will just touch the basics, as you could write books about how to write well designed code - and of course people did.

### Understanding well designed code
So how do you recognize and later down the road write well designed code? Well designed code is easy to read and understand for other human beings. For example the code in the Unity Documentation. Most examples are short and precise. You can look at them and can easily understand how to implement the code. This comes down to many things:
The formatting is precise and blocks of code are indented to make the structure of the code easily recognizeable by skimming over it.
The variable and function names are well chosen. If you had absolutely now idea about coding and someone would ask you what the `Translate()` method does. What would have been your guess? `Rotate()` and `RotateAround()`? As those are examples they have some minimal comments that remind you of the documentation when you decide to copy and paste the code for testing into your project.

### Ending up with good code
So now we have a reference for what well designed code should look like. But how do we end up there?
The first advice I’d like to give is once again: Start on paper! Thinking about what you want to do with your code is essential. Going straight down the road to code is problematic, as it clouds your thinking. Having a list of things your code needs to do on paper will also be a great reference for choosing variable and function names.
You also should not abandon your code as soon as it runs. When you get into the coding frenzy, especially as a beginner, you will try things, comment stuff out and overall have not the knowledge to write beautiful code just like that. And that’s just fine. But dont’t abandon it the moment it actually runs. Then take the time to clean it, massage it and perfect it. There is nothing worse that a piece of code you leave behind, knowing it being a mess. You will not ever want to come back to it and fear the day you have to. Clean up after your done and safe your future self a lot of work!

### Elements of good code: Code Conventions
First of all, naming conventions are team-specific. If you as a team have a good reason to deviate from the language specific naming conventions, then do so. It’s more important to have a consistent codebase to work on, then to follow what everyone else is doing. Yet there are some rules or best practices that spread over the use of a language and it makes sense to abide to these.
Mircosoft has a C# Guidline for this online, but it pretty much boils down to:
- non-static variables/fields and parameters are `camelCase`
- everything else is `PascalCase`
So that’s easy to rather simple to remember, but just have a look at this code as an example.
namespace MyPascalCaseNamespace{
	class MyClass{
		
Code Example?
So 

### Elements of good code: Naming
One of the most important parts in writing good code is the naming of your variables, methods and classes. It all comes down to one thing: use meaningful names. If you had to read the code as a stranger for the first time, would you understand what it does? This means `radius` is better then `r`. If you have a circle and a sphere in your code `circleRadius` and `sphereRadius` would be good choices. Don’t be afraid of long names. By default your code editor is Visual Studio Code, so you have auto-completion as a feature built in. If a long name is more precise, use it!
While a long precise name is fantastic, try not to clutter it with useless information. `radiusOfTheCircle` would just add useless clutter. So as precise as necessary and as short as possible is probably good advice to give.
For variables use adjectives, for methods you should use verbs and for classes nouns as a rule of thumb. This makes sense in the way are used inside your code. When use choose a word for a concept, use the same word for the same concept every time. I.e. you write a custom trigger system, all your functions should use the word tigger in them and not suddenly use event or something like that.
Again this can happen when you are deeply immersed into your coding flow, but when you are done, take step back and take the time to rename those functions and variables. It will make your life and that of other so, so much easier in the long run.

### Elements of good code: Functions
The one hard rule for functions should be: Do one thing. While this sounds very obvious, we often tend to do another thing in the same function. If your function is named `createSphere` then it should not also color them randomly. That’s a different function. It should just do what the name of the function suggest it does.
While assigning the color red would not be a severe problem, as the result would be really obvious, this is especially important for code that is not immediately visible for the user. If you realize your method does more that one thing, go ahead an refactor it.
For function arguments you should try to reduce them as much as possible. There are functions that need to take three variables. Think of a Vector3 for example. You just have to assign x,y and z. But this also means you should never write a function that takes x,y and z as arguments, just pass the function a vector. This removes visual clutter and noise.

### Comments
In a perfect world you would not write a single comment in your code. But we all know the world isn’t perfect. So you will need to write them. But before you start writing a comment, ask yourself: Is there a way to change my code, to make it so well designed, that nobody would need to read this code? Maybe by clarifying a function name?
Well it’ wasn’t possible... Too bad. Then add your comment above the section you want to comment. Make it short and clear and you are good to go.
If you come across comments in code you read, maybe even your own code, ask yourself: Is the comment really describing or adding useful information to the code that follows the comment?
If not, then maybe it should be removed. The thing with comments is: They age really terrible. If you start with a comment for a function and then later change that code because the way you implemented it changes, you might not think about changing the comment. It just happens. So always consider if the comments tell the truth.


Bibliography:
- “Clean Code:A Handbook of Agile Software Craftsmanship” by Robert C.Martin
- Microsoft Framework Design Guidelines (https://docs.microsoft.com/en-us/dotnet/standard/design-guidelines/)
- Unity Documentation

# Optimization #