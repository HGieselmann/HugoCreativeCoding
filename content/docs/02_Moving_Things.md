### On Design
Throughout the first chapters we will use Josef Albers “Hommage to the Square” as a starting point for experimentation. This will be a great way to get started coding with small script and also see how just a few lines of code can change a lot of the feel of things.
These two thing will perfetly go hand in hand, as Design, as well as Coding are Skills. You can read about them as much as you want, but you will only become good at it by actually designing stuff and actually writing code. This is actually an important point. A lot of the ideas of programming are in their core not hard to grasp. A lot of them are really straight forward. What makes programming complex is dividing bigger problems into smaller problems and even smaller problems. And becoming good at this thoughtprocess takes practice. When I went to Drawing school to prepare for my design studies I didn’t get any better until the moment my teacher Ivan forced me to come back with 100 drawings of simple things within a week. The Website drawabox.com has a challenge of drawing 250 boxes.
And for both worlds a great process for starting out exists. In the design world you start out by doing scribbles or storyboards to get an idea of what the result should look like. In coding you should start with so called “Pseudo Code”.
Pseudo Code is just a few written lines of what needs to happen. You can then try ordering them in the way the code would require execution, if you can estimate that. These can just look like your average cooking recipe. In essence they are the same.
I recommend starting on paper, as technology sadly has a tendency to screw with your thinking process, but it can also be a good idea to bring your pseudocode into your script as a comment.

For our “Hommage to the Square” experimentation I started with some simple scribbles on what could be things we could easily do with code:
TODO INSERT SCRIBBLES AND PSEUDOCODE


### Structure of a script

So let’s finally start writing our first script. There are multiple ways to create script, the one I prefer is creating it via `RightClick -> C# Script` in the Project View. The advantage is that, you can directly choose the Folder in which the Script should be located and you don’t have to start organizing your Files afterwards.
But you can also create scripts from the Inspector by adding a component and in the searchPanel simply write the name you want to give to the script. For us that will be “MovingAlbers1” for now.
I guess it is not typical to ad numbers to your scripts, but as we will iterate quite a bit, we will do that for a while.
With your script created just open it using double-click. Your default Code Editor will open. This can take while depending on your system.
{{< expand >}}
## Code Editors and IDEs
The default Code Editor for you probably is “Visual Studio Community Edition” oder “Visual Studio for Mac”. These are IDEs - Integrated Development Environments. These are powerful tools for editing Code, the can integrate with Unity and come with many advanced features. The downside to them is, they tend to be slow. And on a Laptop they can be draining on your battery, as they check code in the background a lot. So if you are on a low end machine it can be wise to look for a “Code Editor”. They are a lightweight alternative, but in comparison lack some advanced features.
Great Code Editors are “Visual Studio Code” by Microsoft, “Atom” by Github.

{{< /expand >}}
Every Unity Script comes with some “boilerplate” Code to get you started. It looks like this:

	using System.Collections;
	using System.Collections.Generic;
	using UnityEngine;

	public class New : MonoBehaviour
	{
	// Start is called before the first frame updat
		void Start()
		{
	
		}
		// Update is called once per frame
		void Update()
		{

		}
	}


The first few lines are “using statements”. These reference Libraries on your computer into the script. And I think libraries is a really fitting word. It’s like quite a bunch of book the computer has read and now you can talk about them and the computer knows what you are alking about. The first two are really like the absolute basics and the “UnityEngine” Library defines all the Unity Specific “book” your computer should know about.

Next up is the class. Every script we write defines a class. You could have multile classes in one and the same file, but that is not considered good practice. Classes really are an advanced topic, so for now, let’s just say they bundle a bunch of code together. Make mark of the MovingAlbers1 as the class name. This corresponds to the name we gave our script file and they always need to have the same name.
Everything that belongs to the class is wrapped inside the following curly brakets. Curly braces define a block of Code. You can see this in the Code for the Start and Update Methods as well. All our code belongs inside theses curly braces - except for any additional using statements.
Speaking of those! Start and Update are Methods that Unity recogizes and calls during the execution of the Program. The Start Function is called first and only once before the program starts running. Here you would define everything you wanted to set up before hand.
The Update Method is then called each frame and keeps running until you end the program. Here we have to write all our Code that changes or animates over the time of the execution of the script.
{{< expand >}}
## What is a Frame?
Images are rendered to your screen, one image at a time. If the distance between two images is short enough we percieve this as fluid motion. Movies are typically shot with 24 Frames per Second. Unity by default is set up to render 60 Frames per Second, which is the most common refreshrate for Monitors.
{{< /expand >}}
In general all your code is executed from top to bottom. So if you would move your using statements to the bottom, Unity or your IDE would start complaining.

### Variables
The first thing Coding Concept we will introduce are variables. Variables are often described as boxes with a name on. You can put stuff in and later retrieve the content of the Box, if you know what’s inside.
In C# variables have a “Type”. This makes C# a (mostly) “type safe” language. To stay with our box example, If you create a box youhave to define what kind of things go inside. A bread box is a bread box and will stay a bread box. A banana box is a banana box and will stay always stay a banana box.
The C# language comes witha few basic types. We don’t need to know about all of them, but others will we use all the time.

#### Numbers
C# comes with eleven (11!) ways to talk of numbers. We will reduce this to three.
{{< expand >}}
## Number-Types and Memory
{{< /expand >}}
The first one is integers. Integers contain all “whole”numbers no matter if positive or negative.
`int integerVariable;`
This code declares an integer variable with the name “integerVariable”. Right now it holds no value and  if would try to access it we would encounter an error.
You can assign to variables using the `=` sign.
{{<highlight c>}}
int integerVariable;
integerVariable = 1;
{{</highlight>}}
This would initialize our integerVariable two 1. 
We could also do this in just one step:
{{<highlight c>}}
int integerVariable = 1;
{{</highlight>}}
Assignment is always done form the rightside of the `=` sign to the left. This also means, that any code on the right side will first be evaluated before it is assigned to the varible on the left.
{{<highlight c>}}
int integerVariable = 1+1;
{{</highlight>}}

Next up are “Floats” and “Doubles”. Both hold all the non-whole numbers. The differnce between the two is, that double use the doubled amount of memory to save values and can store highre precision values. But this also means that  doubles take longer to calculate. That’s why in Unity we use floats, unless we absolutley need to use double precision. So why TALK about doubles already? Because floats are a little weird.
{{<highlight c>}}
float floatNumber = 1.1f;
Double doubleNumber = 1.1;
{{</highlight>}}
Look at that code. See something fishy? 
Whenever we declare a float we have to append the value with a lowercase “f” to tell C# that this is indeed a float-value and NOT a double.
Doubles are the default way to store floating points in C# and C# can’t implicitly convert doubles to floats. So If you do not add the `f` C# will expect the number to be a double.

#### Strings
Another important Data-Type is strings. Strings contain essentially text.
{{<highlight c>}}
string myString = “Hello! I am text.”;
{{</highlight>}}


{{< expand >}}
## Conversion
{{< /expand >}}

#### Objects
Objects are the last important Data-Type we really need to know about. Objects really is a generalization for many things. Unity comes with a lot of types we will use.
The first things we will see are Vectors. 
{{<highlight c>}}
vector3 myVector = new Vector3(1,1,1);
{{</highlight>}}
Vector3s are defined by Unity and essentially bundle 3 floats  in one variable. What’s really important here is the `new` Keyword. It tells C# to allocate some space in memory for it. So if we create variables for classes, then we need to instance them using the new keyword. 
Now this might sound complicated, but you will get the hang of it.

### Starting our first script
So we sketched out what we want to code. So now we just need to transfer those ideas. Earlier we established that the position of an objects is defined through the transform component, so we need to get hold of that one.

To give you a heads up, this is what we will end up with:
![The Unity Editor](/img/movingAlbers.gif)

Because it is used so much, it is really convenient to get to all the transforms.
{{<highlight c>}}
transform.position = new Vector3(0,0,0);
{{</highlight>}}
Transform.position gets hold of the position component of the Object our script is attached to. As position is a vector we need to give it a Vector 3 as input. The `(0,0,0)` are the respective values for X,Y and Z. So this line of code would center all our squares.
Go over to Unity and aadd the Script to all Squares except for the largest one. You can do this via Drag-And-Drop from the ProjectView or via the add Component button on the Inspector. Press Play and all your squares shoud jump to the Center of the scene. As they overlay each other, maybe you can’t see all of them.
In order for them to avoid jumping in the same space, we can hand them their current position in Z back.
{{<highlight c>}}
transform.position = new Vector3(0,0,transform.position.z);
{{</highlight>}}
As we learned the right side is always evaluate before the left side.
{{< expand >}}
## Why not assign a value here?
Because we want to use the same script on all our squares. So we need to make sure all of them get different values.
{{< /expand >}}

To get thing moving, we will make use of some Math-Shenanigans. If you think back to your school days, you know, that te Sin Function always returns a value between -1 and 1; And for a linearly growing value, we get a typical Sinus-Wave.
As in German this is called the “Kreisfunktion” this hopefully fits the idea of the Bauhaus.
So what can we do to get a linear growing value? Well, Time. Just the current time your computer thinks it is.
{{<highlight c>}}
float sinus = Mathf.Sin(Time.time);
{{</highlight>}}
`Time.time` works, because we imported the System.Generic at the top o four script. To apply this as value, we can just set is as one of the values in the Vector3 we create.
{{<highlight c>}}
transform.position = new Vector3(0, sinus, transform.position.z);
{{</highlight>}}

This is great and all, but now all squares move the same distances, but that looks kinda odd, so we need the Offset back, that Josef Albers envisioned of those squares.
We have actually two options to deal with this. We could add a variable to set the offet in the Unity Editor, or we could assume, that alle squares are positioned correctly before the code is running. Let’s look at both:

To create a variable we can create a public variable above our start statement.
{{<highlight c>}}
public float offsetMultiplier = 1;
{{</highlight>}}
	The multiply the sinus with offet.
{{<highlight c>}}
sinus *= offsetMultiplier;
{{</highlight>}}
If you check the Inspector now, you will see a “Textfield”. On each Square you can now define a custom offset. You should be able to just add, the values you chose on the Y Component. You can of course play around with values and try something completley different.
You can also reuse the values you already setup by positioning them in the scene.
To do so read the position value of Y and set it to the offset value in the Start function.
multiplier = transform.position.y;`

The completed Script should look like this:
{{< highlight C >}}
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class MovingAlbersVar : MonoBehaviour
{
	public float multiplier = 1;
		// Start is called before the first frame update
		void Start()
		{
		multiplier = transform.position.y;
			}
		// Update is called once per frame
		void Update()
		{
		float sinus = Mathf.Sin(Time.time) * multiplier;
    
		transform.position = new Vector3(transform.position.x, sinus,transform.position.z);
		}
	}
{{< / highlight >}}

- learn parenting
- 