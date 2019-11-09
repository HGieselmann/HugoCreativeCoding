# 10 - Problem Solving and well designed code
### Designing Code
Before we dive deeper into considerations of design, let’s take a very short break and discuss designing code. As with design, there are often different ways to solve the same problem. You soon will, or already have seen, me writing code that you would have approached differently. And it is possible that your solution is better. (And please let me know if you think I do some stupid stuff!! “LinkToContactSheet”) But maybe it’s just a different approach to the problem. Five programmers will solve the same problem in 5 different ways. And that’s fine.
However, there can also be differences in the effort put in to solving the problem. Yes, you can solve many problems naming your variables `x1` to `xn`. But will you remember what `x1` and `x2` were, when you look at your code one month later? You probably can’t. You will have to read through that and figure out what these variables were used for.
This chapter is devoted to some basic conventions about writing beautiful code. We will just touch the basics, as you could write books about how to write well designed code - and people did. Most notably, Robert C. Martin. He describes many of the following ideas and concepts in his book “Clean Code” in great detail. So if you want to further you understanding after this chapter, check it out!

### Understanding well designed code
So how do you recognize and write well designed code? Well designed code is easy to read and understand for other human beings. The code in the Unity Documentation is a great example. Most examples are short yet on point. They are easy to skim through and learn from. This comes down to many things:
The formatting is precise and blocks of code are indented to make the structure of the code recognizable just by skimming over it.
The variable and function names are well chosen. If you had no idea about coding and someone would ask you what the `Translate()` method does. What would have been your guess? `Rotate()` and `RotateAround()`? As those are examples they have some minimal comments that remind you of the documentation when you copy and paste them into your project. They are a fantastic learning resource.
But you will also find great examples on GitHub and other code resources. Whenever you feel the code you see is readable and you can easily understand it, you have some good code in front of you.

### Ending up with good code
Now we know what well designed code looks like. But how do we end up there?
The first advice I’d like to give is once again: Start on paper! Thinking about what you want to do with your code is essential. Going straight down the road to code is problematic, as it clouds your thinking. Having a list of things your code needs to do on paper will also be a great reference for choosing the variable and function names. With time you can more and more reduce this way of working, but as a beginner it helps a lot! And for more complex work it’s a valuable way of working as a professional.
You also should *not* abandon your code as soon as it runs. When you get into the coding frenzy, especially as a beginner, you will try things, comment stuff out and overall have not the knowledge to write beautiful code just like that. And that’s just fine. But don’t abandon it the moment it runs. Take the time to clean it, massage it and perfect it. There is nothing worse than a piece of code you leave behind, knowing it is a mess. You will never want to come back to it and fear the day you have to. Clean up after you’re done and safe your future self a lot of work!
*But* don’t over do it. Clean and minimalistic. Just because you know how to write properties, you don’t have to use them if a simple public variable does the trick. For now you are in a game engine and not writing car automation systems.

### Elements of good code: Code Conventions
First, naming conventions are team-specific. If you as a team have a good reason to deviate from the language specific naming conventions, then do so. It’s more important to have a consistent code base to work on, then to follow what everyone else is doing. Yet there are some rules or best practices that spread over the use of a language and it makes sense to abide to these.
Microsoft has a C# Guideline for this online, but it boils down to:
- non-static variables/fields and parameters are `camelCase`
- everything else is `PascalCase`
So that’s easy to remember, but just have a look at this code as an example.
namespace MyPascalCaseNamespace{
	class MyClass{
		
Code Example?
So 

### Elements of good code: Naming
One of the most important parts in writing good code is the naming of your variables, methods and classes. It all comes down to one thing: use meaningful names. If you had to read the code as a stranger for the first time, would you understand what it does? This means `radius` is better than `r`. If you have a circle and a sphere in your code `circleRadius` and `sphereRadius` would be good choices. Don’t shy away from of long names. By default your code editor is Visual Studio, so you have auto-completion as a feature built in. If a long name is more precise, use it!
While a long precise name is fantastic, try not to clutter it with useless information. `radiusOfTheCircle` would just add useless clutter. So as precise as necessary and as short as possible is good advice to give.
For variables use adjectives, for methods you should use verbs and for classes nouns. This makes sense in the way they are used in your code. When you choose a word for a concept, use the same word for the same concept every time. I.e. you write a custom trigger system, all your functions should use the word *trigger* in them and not use *event* or something like that.
Again this can happen when you are immersed into your coding flow, but when you are done, take a step back and take the time to rename those functions and variables. It will make your life and that of others so much, much easier!

### Elements of good code: Functions
The one hard rule for methods should be: Do one thing. While it sounds very obvious, we often tend to do another thing in the same method. Take a method named `createSphere()`. It should create a sphere. It shouldn’t color them randomly as well. That’s a different method. It should just do what the name of the method suggest it does.
Now you might say, everyone *sees* that the sphere is i.e. red. That’s true, but most problems aren’t that drastically visual. For other users of your methods this can end badly! 
Thus, if you realize your method does more that one thing, refactor it.
For method arguments you should try to reduce them as much as possible. There are methods that need to take three variables. Think of a Vector3 for example. You just have to assign x, y and z. But in most cases you can avoid this. If you have to pass more than one or two variables to a method, think about it. Can you clean this up more?

### Elements of good Code: Comments
In a perfect world you would not write a single comment in your code. But we all know the world isn’t perfect. So you will need to write them. But before you write a comment, ask yourself: Is there a way to change my code, to make it so well designed, that nobody would need to read this comment? Maybe by clarifying a function name?
Well, it’ wasn’t possible... Too bad. Then add your comment above the section you want to comment. Make it short and clear and you are good to go.
If you come across comments in code you read, maybe even your own code, ask yourself: Is the comment describing or adding useful information to the code that follows the comment?
If not, remove it. The thing with comments is: They age terrible. If you start with a comment for a function and then later change that code because the way you implemented it changes, you might not think about changing the comment. It just happens. So always consider if the comments tell the truth.


Bibliography:
- “Clean Code: A Handbook of Agile Software Craftsmanship,” by Robert C. Martin
- Microsoft Framework Design Guidelines (https://docs.microsoft.com/en-us/dotnet/standard/design-guidelines/)
- Unity Documentation

# Optimization #