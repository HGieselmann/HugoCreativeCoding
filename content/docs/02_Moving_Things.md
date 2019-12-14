# 02 - Moving Things
Before we get started: It is easy to get lost in code as a beginner. There are many things that can throw you off, so it really is a good idea to have an exact plan on what you want to achieve. These can just be some doodles or scribbles, just anything that will get you away from the code and into your personal design thinking space. <br>
{{< figure src="/img/Scribbles.jpg" title="Scribbles" width="50%">}}
These are some of the scribbles I first created when thinking about these cuboids that will be following us throughout this book. These aren’t beautiful, they are just quick. A Quick representation of what you could do with one cuboid and a basic transform. <br>
Now you might think these redundant and unnecessary, but they are a simple way to remind you of what you wanted to create in the first place. They also help to quickly iterate ideas before you go in and have to deal with actually coding.<br>
Another great way to prepare yourself for coding is writing down in your native language what should happen inside your program. This can really help to structure your code beforehand and identify problems or hard to solve issues before you sit down and write your code. <br>
*“If you press ‘A’ the player should jump. If he hits an enemy he loses a life.”* <br>
Superbly simple and yet you now know, you need a player character thats able to jump, you need to check for Input, you need to keep track of lives and find a way to check collision with an enemy player. That is a lot of information in just a simple sentence. <br>
Both of these processes might seem excessive they really help you get some distance and reflect about the problem at hand in a more concentrated way, so I hope you will at least try these out. But anyway, let’s get to it!


### Structure of a script

So let’s start writing our first script. There are multiple ways to create a script, the one I prefer is creating it via `Right-click -> C# Script` in the Project View. The advantage here is: you can choose the folder in which the Script should be located and you don’t have to start organizing your files after the fact. <br>
But you can also create scripts directly from the Inspector by clicking on “Add Component” and in the search panel simply write the name you want to give to the script. If there isn’t any other component or script with the same name in your project Unity will assume you want to create a script with that name. I called my first script: “MovingCuboids_Lifting”. <br>
With your script created just open it using double-click. Your default Code Editor will open. This can take a while depending on your system, especially when you open the editor for the first time.
{{< expand >}}
### Code Editors and IDEs
The default Code Editor for you probably is “Visual Studio Community Edition” or “Visual Studio for Mac”. These are so-called “IDEs” - Integrated Development Environments. These are powerful tools for editing Code, they can integrate with Unity and come with many advanced features. The downside to them is, they tend to be slow to start up. And on a laptop they can be draining on your battery, as they thoroughly check your code in the background. So if you are on a low end machine it can be wise to look for a “Code Editor”. They are a lightweight alternative, but in comparison lack some advanced features. <br>
Great Code Editors are “Visual Studio Code” by Microsoft or “Atom” by GitHub, which is also part of Microsoft. There is also Sublime Text. <br>
If you want to check out an IDE that is becoming more and more popular with Unity programmers look out for “Rider” by JetBrains. They also offer the very helpful Plug In “ReSharper” for Visual Studio.
{{</expand >}}
Every Unity Script comes with some “boilerplate” Code to get you started. It looks like this:


{{<highlight c>}}

	using System.Collections;
	using System.Collections.Generic;
	using UnityEngine;

	public class MyNewClass : MonoBehaviour
	{
	// Start is called before the first frame updates
		void Start()
		{
	
		}
		// Update is called once per frame
		void Update()
		{

		}
	}
{{</highlight>}}



The first few lines are “using” statements. All lines in C# that end with a semicolon are considered a “statement”. The “using” statements reference “namespaces” or libraries on your computer into the script. And I think libraries is a nice description for it. Think of it like a book club and you define beforehand which books you want to talk about. It’s tedious to talk about “The Lord of the Rings” if the other person hasn’t read the book. <br>
Using these statements you expect Unity know about everything in the UnityEngine itself, as well as the chapters “Collections” and “Collections.Generic” from the “System” book. You can see we can access or require sub-parts using the so called “dot notation”.

Next up is the class. Every script we write defines a class. You could have multiple classes in the same file, but that is not considered good practice in C#. Classes really are an advanced topic, so for now, let’s just say they bundle a bunch of code together. Take note of the MovingCuboids_Lifting as the class name. This corresponds to the name we gave our script file and they always need to have the same name. If you change the classname, you have to change the filename and vice versa. <br>
Everything that belongs to this class is wrapped inside the following curly brackets. Curly braces define a block of Code. You can see this in the Code for the Start and Update Methods as well. All our code belongs inside the curly braces of the class, except for everything related to namespaces.

Moving on to “Methods”. Start and Update are Methods that Unity recognizes and calls during the execution of the program. The Start function is called first and only once before the program starts running. Here you would define everything you wanted to set up. <br>
The Update method is then called each frame and keeps running until you end the program. Here we have to write all our Code that changes or animates over the time of the execution of the script.

{{< expand >}}
## What is a Frame?
Images are rendered to your screen, one image at a time. If the distance between two images is short enough, we perceive this as fluid motion. Movies are typically shot with 24 Frames per Second. Unity by default is set up to render 60 Frames per Second, which is the most common refresh rate for Monitors.
{{< /expand >}}
In general all your code is executed from top to bottom. So if you would move your using statements to the bottom, Unity or your IDE would start complaining.

That concludes our first little overview of script structure.

### Variables
The first thing Coding Concept we will dissect in detail is “Variables” . Variables are often described as boxes with a name on. You can put stuff in and later retrieve the content of the Box. You can store pretty much anything in variables.

In C# variables have a “Type”. This makes C# a (mostly) “type safe” language. To stay with our box example, If you create a box you have to define what kind of things go inside. If you happen to have a heart-shaped box, you can only store heart-shaped things in there. If you create a round box, you can only store round things in it.

#### Numbers
C# comes with eleven (!) ways to talk about numbers. We will simplify this and only talk about three of them.
{{< expand >}}
#### Number-Types, Memory and Performance
The reason C# incorporates so many types of numbers lies in all the different use-cases of the language. You might write an application that needs to deal with super precise numbers, or especially large numbers. But these take more space in memory and take longer to calculate. In a game engine like Unity most of the time ultimate precision isn’t important, but performance is. Thus you need to choose the type of number based on your need. You will only need to concern yourself with these in later stages of your programming journey.
{{< /expand >}}
The first one is integers. Integers contain all “whole” numbers no matter if positive or negative.
{{<highlight c>}}
int integerVariable;
{{</highlight>}}
This code declares an integer variable with the name “integerVariable”. Right now it holds no value and if would try to access it, you would encounter an error. <br>
You can assign values to variables using the `=` sign.
{{<highlight c>}}
int integerVariable;
integerVariable = 1;
{{</highlight>}}
This would initialize our integerVariable to “1”. <br>
We could also do this in just one step:
{{<highlight c>}}
int integerVariable = 1;
{{</highlight>}}
Assignment is always done form the right side of the `=` sign to the left. This also means, that any code on the right side will first be evaluated before it is assigned to the variable on the left:
{{<highlight c>}}
int integerVariable = 1+1;
{{</highlight>}}
`integerVariable’ would now hold the value “2”. <br>
Next up are “floats” and “doubles”. Both hold all the non-whole numbers. The difference between the two is, that double use the double amount of memory to save values and can store higher precision values. But this also means that doubles take longer to calculate. That’s why in Unity we typically use floats, unless we absolutely need double precision. So why even TALK about doubles already? Because floats are a little weird...
{{<highlight c>}}
float floatVariable = 1.1f;
Double doubleVariable = 1.1;
{{</highlight>}}
Look at that code. See something fishy? <br>
Whenever we declare a float we have to append the value with a lowercase “f” to tell C# that this is indeed a float-value we want to use and **not** a double. 
{{<highlight c>}}
float floatVariable = 1.1;
{{</highlight>}}
If we don’t do this, our code will actually not run! The above line will cause an error. The compiler can’t know which value it is, we want to store inside and if he assumes that there is a chance, that he would have to lose data in the process of converting on type to the other, he won’t do it. <br>
The compiler will though convert values from one type to the other if he can be sure that no data loss can happen. This is called “implicit” conversion. Implicit conversion happens from integers to floats and floats to doubles and of course integers to doubles. <br>
If you want to force conversion for types it’s called “explicit” conversion and we do this using a “cast”:
{{<highlight c>}}
float floatVariable = (float)1.1;
int intVariable = (int)0.5;
{{</highlight>}}
You can use this syntax whenever you need to do a simple conversion between values. But note, that while the second statement works, you will have data loss!! So use them carefully!

#### Strings
Another important Data-Type is strings. Strings contain essentially text.
{{<highlight c>}}
string myString = “Hello! I am text.”;
{{</highlight>}}


{{< expand >}}
#### Conversion
{{< /expand >}}
What needs to be said about strings, really???

#### Objects
Objects are the last important Data-Type we really need to know about. Objects really is a generalization for many things. Unity comes with a lot of types we will use.

The first things we will see are Vectors. 
{{<highlight c>}}
vector3 myVector = new Vector3(1,1,1);
{{</highlight>}}
Vector3s are defined by Unity and essentially bundle three floats in one variable. What’s really important here is the `new` Keyword. It tells C# to allocate some space in memory for it. So if we create variables for classes, then we need to instance them using the new keyword. 

Now this might sound complicated, but for now just roll with it. We will look deeper into this once we reach the chapter about classes and object orientation.

### On Pseudo Code
Throughout the first chapters we will use our “Homage to the Cuboid” as a starting point for experimentation. This will be a great way to get started coding with very small scripts and also see how just a few lines of code can create interesting results. <br>
But before you actually start to code, it’s often a great idea to think about what you want to achieve. There is also great value putting this down on paper. So let’s look at the options we have right now. We have been looking at the transform component in the editor, and this gives us exactly nine values to manipulate: X,Y and Z for each transformation: translation, rotation and scale.

TODO Sketch of possible actions:
So let’s start with translation, bringing a little snake-like movement into our homage. We will aim for something like this:
{{< figure src="/img/MovingCuboids_Shifting_X.gif" title="Cuboids Shifting on the X Axis" width="50%">}}
Now that we have a creative vision let’s start out with something called “Pseudo Code”. Pseudo code is the idea of writing something code like, but on a really high level. An abstraction which will make it easier to write the code itself later. You can use comments in your code to put down pseudo code. Comments start with double slashes `//` and everything that follows in that line will ignored by the compiler.

We know that we can assign values to variables, and that we only want to change the value on one axis, so let’s use the X axis for now.
{{<highlight c>}}
// x = 
{{</highlight>}}  
How do we get the swinging motion? We’ll make use of a useful thing you might remember from school: A sine wave. 
The `sin()` method will continuously create a value for us between 0 and 1. Where can we get a continuously growing value? Well: Time! So some simplified code could look like this:
{{<highlight c>}}
//x = Sinus of Time
{{</highlight>}}
This is actually the basic idea. Now that we have that, we need to figure out how to create the offset between each of the Cuboids. We have to create some kind of Offset for them. But what do we have to Offset? If we Offset X as a whole, we just move the cuboids apart, we actually need to offset the value the `sin()` function creates and thus need to offset the time value itself. We will also need to be able to adjust this value for each Cuboid individually. 
{{<highlight c>}}
// pseudo Code
//x = Sinus of (Time + Offset per Cuboid)
{{</highlight>}}
So let’s get coding!

### Starting our first Script
So let’s tackle this in the same order as our pseudo code. We need to access the X axis. To access the transform component of the object our script is attached to Unity luckily provides us with a nice shortcut: we can simply use `transform`. To access sub-components we use “dot notation”, like this:
{{<highlight c>}}
transform // gets the transform component itself
transform.position // gets the position of the component as a Vector3
transform.position.x // gets the X position as a float.
{{</highlight>}}
And while we can “get” the X position this way, Unity doesn’t actually allow us to modify the value this way. We need to set the position as a whole and thus as a Vector3.
{{<highlight c>}}
void Update(){
	transform.position = new Vector3(0,0,0);
}
{{</highlight>}}
This would set all our transform values to zero. But as we said, we only want to change the value for the X axis. So let’s make sure that happens, by retrieving the current Y and Z values.
{{<highlight c >}}
	transform.position = new Vector3(0, transform.position.y, transform.position.z);
{{</highlight>}}
This code will set our X value to 0, but retain the current values for Y and Z and thus all our positioning we did in the Unity Editor for these axis will stay put.

Now to get our motion going, we need to get a hold of time and calculate the sin. Time we can grab from the Time object using `Time.time`. To calculate a sin from it we can access the “Math” class using `Mathf`.
{{<highlight c>}}
	float sin = Mathf.Sin(Time.time);
{{</highlight>}}
Here we calculate the Sin value of the current time and store it in a float variable called `sin`. We can then go on and assign it to our X position in the Vector3:
{{<highlight c>}}
	float sin = Mathf.Sin(Time.time);
	transform.position = new Vector3(sin, transform.position.y, transform.position.z);
{{</highlight>}}
{{< figure src="/img/MovingCuboids_Shifting_X_Intermediate.gif" title="Well... it’s a start..." width="50%">}}
While we are still missing the offset, we also have a very strong movement, and we might want to control both of these.

### Public and private variables
In our pseudo code we found, we need to create an offset for each of our Cuboids. And while we **could** go ahead an create a script for each of them, that would be very tedious work. It would also be a very awful violation of the “DRY” programming principle: “Don’t repeat yourself!”. Thus what we need is a variable we can adjust per Cuboid.

We will put this variable above the Start function but inside the class:
{{<highlight c>}}
public class MovingCuboidsShifting : MonoBehaviour
{
    
    public float timeOffset = 0;
    void Start()
    {
	}
}
{{</highlight>}}
Notice something new? We just made our variable `public`. Public variables can mainly be seen and set by other scripts. But in Unity they also show up on the component in the Inspector.
{{< figure src="/img/ExposedVariables.jpg" title="Variables exposed in the Inspector" width="50%">}}
So now we can set this value for each Cuboid separately. By default all variables and functions are private and you don’t need to put the private keyword. But sometimes it helps to clarify your code.
{{< hint info>}}
### Serialize Field
But, the `public` keyword does more than just exposing the variable to the Unity Editor. It will allow other scripts in your project to access this variable and read it or change it. And this is a gateway opening up for bugs. Taht’s why we want keep our variables `private` as possible. To remedy this problem Unity offers the Tag `[SerializeField]`. It will expose your variable to the Unity editor and keep in private for other scripts. Win - Win!
{{<highlight c>}}
[SerializeField]
private float timeOffset = 0;
{{</highlight>}}
This is the preferred way of working. And while it may seem like unnecessary clutter for now, this will make your life easier down the road. Using this workflow, all the decisions you make regarding making variables public will be conscious.
{{</hint>}}

### Variable Scope
The last thing regarding variables we need to talk about is “variable scope”. Scope is about which you are able to access at which point in your code. In our code we at the moment have two places in which we create variables. On top of the class and inside the Update loop. Variables you create at the top of the file, or to be precise directly inside the `{}` of the *class* have “global scope”. They can be accessed in any function or loop in the class. <br>
Variables you create inside a method like `Update()` or `Start()` have “local scope”. The can only be accessed inside the method or loop they were created in.<br>
{{<highlight c>}}
public class exampleClass : MonoBehaviour{
	private int myInteger = 0; // This is at global scope
	Start(){
		private int myOtherInteger = 0; // This is at local scope
		myInteger = 1; // This works
		myOtherInteger = 1; // This works as well
	}
	Update(){
		myInteger = 2; // This works
		myOtherInteger = 2; // This DOES NOT WORK!! 
	}
{{</highlight>}}
In general you have access to the variables declared on “level”up and at the same level but you don’t have access to the variables at one finer level of detail. They are “out of scope”.

### Putting it in practice
Now that we have a value we can adjust, let’s incorporate it into our script:
{{<highlight c>}}
[SerializeField]
private float timeOffset = 0;
    void Update()
    {
        float sinus = Mathf.Sin(Time.time + timeOffset);
        transform.position = new Vector3(sinus, transform.position.y, transform.position.z);
    }
{{</highlight>}}
Now look at the placement of our offset. What do you think would happen if put it outside of the parentheses? All operations in C# follow the basic rules of precedence, but if you’re in doubt about them feel free to just add more parentheses.

Lastly we want to add a scaling factor on the movement range of the cuboids:
{{<highlight c>}}
float movementScale = 0.25f;
{{</highlight>}}
No we can ask the interesting question where to put this. And there are actually many options, but let’s consider the obvious ones:
{{<highlight c>}}
[SerializeField]
private float timeOffset = 0;
float movementScale = 0.25f;
    void Update()
    {
        float sinus = Mathf.Sin(Time.time + timeOffset) * movementScale;
        transform.position = new Vector3(sinus, transform.position.y, transform.position.z);
    }
{{</highlight>}}
And:
{{<highlight c>}}
[SerializeField]
private float timeOffset = 0;
float movementScale = 0.25f;
    void Update()
    {
        float sinus = Mathf.Sin(Time.time + timeOffset);
        transform.position = new Vector3(sinus * movementScale, transform.position.y, transform.position.z);
    }
{{</highlight>}}
Or the one I actually like best:
{{<highlight c>}}
[SerializeField]
public float timeOffset = 0;
float movementScale = 0.25f;
    void Update()
    {
        float sinus = Mathf.Sin(Time.time + timeOffset);
        sinus = sinus * movementScale;
        transform.position = new Vector3(sinus, transform.position.y, transform.position.z);
    }
{{</highlight>}}
When and where you put your operations depends on the situation, partly depends on style but should mostly be about readability. Which of these would you think is most clear to any other person reading this?

You could even go so far as to create a completely new variable for the scaled sinus, which is very precise and thus a very good way to write your code.
{{<highlight c>}}
[SerializeField]
private float timeOffset = 0;
float movementScale = 0.25f;
    void Update()
    {
        float sinus = Mathf.Sin(Time.time + timeOffset);
        float scaledSinus = sinus * movementScale;
        transform.position = new Vector3(scaledSinus, transform.position.y, transform.position.z);
    }
{{</highlight>}}
Whichever way you choose. You should now have something like this happening. You can pat yourself on the back. All of this an important first step!
{{< figure src="/img/MovingCuboids_Shifting_X.gif" title="Cuboids Shifting on the X Axis" width="50%">}}

### Rotation
While scaling will be very similar to what we just did, rotation can be a little harder. But this is totally dependent on your needs. If you only need to rotate an object around an axis, rotation can be as simple as:
{{<highlight c>}}
transform.Rotate(0, 1, 0);
{{</highlight>}}
This would rotate the object around the Y axis by a given value.<br>
What you can’t do however is assign a Vector3 directly to the Rotation value. Rotations in Unity are stored in Quaternions. Quaternions take in four values and help in avoiding some problems with rotations in 3D space. To set Rotation values, you would need to use this method:
{{<highlight c>}}
transform.rotation = Quaternion.Euler(0,1,0);
{{</highlight>}}
{{< figure src="/img/MovingCuboids_Rotating25.gif" title="RotatingCuboids" width="50%">}}

Add Parenting rotation Script here
The key to recreating this sketch in parenting. We can simply place a planet at the center of the scene (Position 0/0/0) and add a script to rotate it. We can also use this script and attach it to an “empty GameObject” at the center of the scene. This is a very common way to set up relationships in 3D. If you look at the Rockets themselves you will see, that they are set up in the exact same way. This will allow us to have some control still over the objects inside Unity.
{{<expand>}}
{{<hint info>}}
Once you get to the point where your scenes become very, very complex or you are aiming for mobile deployment, it is advisable to keep hierarchies relatively shallow for performance reasons. For now this not an issue though.
{{</hint>}}
{{</expand>}}

### Projects
Project 1 - Variants
To conclude this chapter I again would like to ask you to spend some time and play with the concepts you learned in this chapter some more. Here are some things I came up with you could achieve only using the concepts we introduced so far.
{{< figure src="/img/MovingCuboids_ScalingXZ.gif" title="Cuboids Scaling on X and Z" width="50%">}}
{{< figure src="/img/MovingCuboids_ScalingY.gif" title="Cuboids moving on the Y Axis" width="50%">}}


Project 2 - Space Exploration
{{< figure src="/img/SpaceExploration.gif" title="Space Exploration" width="50%">}}
This project is a little more advanced as it uses external models again and you will need to make use of parenting in the hierarchy view. <br>
Download the Assets here: <br>
Add Assets here!
The key to recreating this sketch in parenting. We can simply place a planet at the center of the scene (Position 0/0/0) and add a script to rotate it. We can also use this script and attach it to an “empty GameObject” at the center of the scene. This is a very common way to set up relationships in 3D. If you look at the Rockets themselves you will see, that they are set up in the exact same way. This allows us to still have some kind of control over the objects in Unity. I.e we could scale the legs of windows of the spaceships to our liking.
{{<expand>}}
{{<hint info>}}
Once you get to the point where your scenes become very, very complex or you are aiming for mobile deployment, it is advisable to keep hierarchies relatively shallow for performance reasons. For now this not an issue though.
{{</hint>}}
{{</expand>}}
You can now position the spaceship somewhere in the orbit of the planet. Once you switch to playmode your spaceship should fly around the planet in the way you set up the empty in object in the center.
For the flame we can again just go ahead and create a script that oscillates the size. We can also add our Rotation script to give even more liveliness to the flames. But this is all up to you and your creativity. <br> 
Important to see here is how much you can actually create with just a few very small scripts attached to objects. <br>
You can then go ahead and play with materials, colors and lights for your scene. I personally think it can be especially fun to play with the camera and get interesting views on one and the same sketch. That’s one of the great things about working in three dimensions of course!
{{< figure src="/img/SpaceExploration2.gif" title="Space Exploration 2" width="50%">}}
Add Asset of completed Scene here



