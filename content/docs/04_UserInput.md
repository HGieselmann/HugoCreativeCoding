Title: Master  
Author:   


### Conditionals
So we kow how to code some absolute basic movement. But that’s built upon the conveneience of the Sin Function and that’s really rather limited.
So what if we could do things based off of some condition. Let’s say you press a button, move the mouse or tilt your phone?
This is where Conditionals come in. Conditionals are one way to manage how your code is flowing (”Control Flow”). They manifest them self in “If” and “If-Else”-Statements. Meaning that you can define code that runs only if a certain condition is met. Or code which runs when a condition is met, but also has a fixed Block of code which will run instead.
With the introduction of conditionals we also need to introduce another variable type: The Boolean. Luckily this one is really easy to grasp. It knows exactly two states. True or false.
If statements the are pretty straight forward: You start with `if` followed by a condition in brackets and the put the Code to execute on condtion in the following curly brackets.
{{< highlight c >}}
// Declaring and initializing some booleans
private bool myBoolean = true;
private bool myboolean2 = false;
if(myBoolean){
	// Code to execute on condition
	// This Code would run
}
if (myBoolean){
	// Code to execute on condition
	// This code would not run
}
{{< / highlight  >}}
So can use boolean variables as your condition on your if-statements. You can also put statements that either evaluate to true or false. To do this C# offers conditional operators. You probably remember some of these form school: 
`>` greater then
`<` smaller then
`>=` greater or equal
`<=` smaller or equal
`==` is equal to
`!=` not equal to
What’s to note here is that `==` or double-equals is for checking If some values are equal, becaus single`=` is already used for assigning variables. 
{{<highlight c>}}
If(1<2){
	// Code block
	// This code will run
	}
If(1>2){
	// Code block
	// This code won’t
	}
{{</highlight>}}

Of course we can put any statement in those brackets. To pick up where we left of last chapter, let’s create a condition based on our sinus function:
if (sinus > 0)
{
	transform.position = new Vector3(transform.position.x, sinus,transform.position.z); 
}
This way we will only get the animatin from center to top and then a hold at the center position. While it is working, it isn’t really a visually pleasing result.
So let’s think about other ways we could use Conditionals to improve our Sketch. A contra-movement on one of the Squares could be interesting. One way to achieve his would be to, have a whole different script act on that Square. Or we could just have a public Boolean which could be checked to inverse the motion.
{{< highlight c>}}
...
public class MovingAlbers : MonoBehaviour {     public float multiplier = 1;     public bool inverse = false;      // Update is called once per frame     void Update()     {         float sinus = Mathf.Sin(Time.time) * multiplier;         if (inverse)         {             sinus *= -1;         }                  transform.position = new Vector3(transform.position.x, sinus,transform.position.z);     } }
{{</highlight>}}


### Getting User Input
As Unity is in it’s core a game engine one of it’s core features is of course to do something based on User Input. Every game obviously needs this way of interaction. Unity kindly exposes many differnt ways to get Inout from the user and we will cover the most important here.
{{<highlight c>}}
if (Input.GetKey(KeyCode.A)) {     transform.position = new Vector3(transform.position.x, sinus,transform.position.z);  }
{{</highlight>}}
The return-type for these is often a boolean. So this Code will execute as long as you you press the “A” Key on your Keyboard. Unity offers a variety of  Methods. I.e. you could check for the moment you pressed the Key `Input.GetKeyDown()` or the moment you release the Key `Input.GetKeyUp()`.
No let’s again think about beautifying our result. Right now the moment we press the “A” Key all our squares jump and then keep moving. A more pleasing result would bet to have the starting of where we left off. So let’s think about our code. Where exactly does the movement come from?
The movement is ingrained in our usage of time as a variable. Even worse. It is using System time, and that’s really a place we can’t and don’t want to stop!
We need to create our own way of advancing time. We can do that with a simple float variable.
{{<highlight c>}}
private float timePressed = 0;
{{</highlight>}}
Now, we could go ahead and just add a small value to our timePressed Variable. And we would get a seemingly smooth Animation. This would work fine as long as our machine is able to maintain a constant framerate. By default it is limited to 60 Frames per Second as a maximum. So worst case, we would get a slower animation on slower computers. But we could disable this upper Limit and on new computers it could easily run ten times faster.
This is actually a very common problem in 3D Engines. The fix programmers came up with, is deltaTime. DeltaTime is the time that passed since the completion of the last frame. If you add the deltaTime of each frame over the timeframe of a second, you should end up with more or less a second. By all means this isn’t perfect, but it’s as good as it gets. And as long your computer doen’t have any hicups, this will be fine.
{{<highlight c>}}
if (Input.GetKey(KeyCode.A))
{
    timePressed += Time.deltaTime;
}
{{</highlight>}}
Now you can use timePressed instead of Time.time in your sin-Function. And the Animation should continue where it left of.

The if-statements we looked at so far, always were deciders for one block of code, but they can also behave like a fork in the road with if-else-statements.
{{<highlight c>}}
	// Code for if-else for inverse based on Keypress
{{</ highlight>}}

They can even check for additional conditions.
{{<highlight c>}}
	// Code for if-elseIf-else statements
{{</highlight>}}

Sometimes it is necessary to have multiple if-statements stacked into each other. And this works fine, but you should avoid going deeper then to levels. This will make debugging your code really hard and messy and there are very likely other ways to deal with that sort of complexity.
TODO
IMPLEMENT COLOR CHANGES HERE!








