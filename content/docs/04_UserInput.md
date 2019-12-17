# 04 - Conditionals
So we know how to code some absolute basic movement. But all of that is built conveniently on the `Sin()` function and it will just always run, we have no way of interacting with it. \
What if we could do things based off of some condition. Let's say you press a button, move the mouse or tilt your phone? \
This is where "Conditionals" come in. Conditionals will manage how your code will "flow", and they belong to a group of programming ideas that people refer to as "Control Flow". Conditionals in their widest used form come as "if-else" statements. The ideas is, to run code if a certain condition is met - a.k.a "true". You can then have a statement that defines what happens if the condition turns out not to be true, but that's not a hard requirement.
{{<highlight c>}}
if(true){
	// This Code would run
}
if (false){
	// This code would not run
}
{{< / highlight  >}}
As you can see, the syntax for this is pretty straight forward. You start out with a simple `if` put `true` or `false` in parentheses and add your code in curly braces.\
While this is perfectly valid code, it's also pretty nonsensical. The first condition is `true` and will always be `true` and the second piece of code will never run. That makes no sense at all!\
To make sense of this we need to introduce a new Type: The boolean. Exactly like floats or integers you can create variables for booleans and do "calculations" with them. Yet these calculations need to return `true` or `false`. Here are some example:
{{<highlight c>}}
bool myBool = 2 > 1; //returns True;
bool myOtherBool = 2 < 1; //returns False;
{{</highlight>}}
You can actually use a few of these operators:\
`>` greater then\
`<` smaller then\
`>=` greater or equal\
`<=` smaller or equal\
`==` is equal to\
`!=` not equal to\
While all of these are pretty straight forward I want to point your attention shortly on the "is equal to" operator. It uses double equals. As you know we already have single equals in use to assign values to variables, thus double equals is required for comparison.\
Using boolean variables or expressions in the parentheses we can make these if statements actually useful. For example we could check if the sinus value on our moving cuboids is negative and then inverse it into a positive number:
{{<highlight c>}}
if (sinus < 0){
	sinus  = sinus *-1;
}
{{</highlight>}}
In the above code the expression `sinus < 0` would evaluate to a boolean of either `true` or `false`. Leading to a bouncing motion of the cuboids, as we essentially mirror the negative values of sinus into positive values.
{{< figure src="/img/04MovingCuboids_ShiftingX.gif" title="Mirrored X Animation" width="50%">}}
*If-statements* also come in two more variants: *If-else* and *If-if else-else*. The idea behind these should be pretty clear from the naming itself, but let's explore them in detail. While a single *if-statement* will just return to the main-body of code if the condition isn't met, an else statement will execute another piece of code. Think of an amusement park ride. You are either tall enough and can enter or you are too short and will be send away...
{{<highlight c>}}
bool isAllowedOnRide;
float height = 150; // in cm
if (height >= 150){
	isAllowedOnRide = true;
	Debug.Log("You are tall enough. Enjoy the ride.");
}else{
	isAllowedOnRide = false;
	Debug.Log("You are too small, kid. Sorry...);
}
{{</highlight>}}
This code would make sure either one of both blocks is run. \
The last option are *If-else if-else* statements, in which you you could actually have as many *else ifs* as you like. An example could be a code that checks which team won in a football match, or if the match ended in a tie.
{{<highlight c>}}
int TeamAGoals = 2;
int TeamBGoals = 0;
if (TeamAGoals > TeamBGoals){ 	DebugLog("Team A Wins!");
}else if (TeamBGoals > TeamAGoals){
	Debug.Log("Team B Wins");
} else {
	Debug.Log("Tie!");
}
{{</highlight>}}
We can of course make use of these in our Homage to decide for one approach or another using these statements. 
Based on a boolean we promoted to the Editor we can offset the bouncing direction.
{{<highlight c>}}
using UnityEngine;

public class ConditionalCuboidsShiftingXZAppartSimple : MonoBehaviour
{
    [SerializeField]
    private float timeOffset = 0;
    [SerializeField]
    private float movementScale = 0.25f;
    [SerializeField]
    private bool inverted;
    void Update()
    {
        float sinus = Mathf.Sin(Time.time + timeOffset);
        sinus = sinus * -1;
        sinus *= movementScale;
        if (inverted)
        {
            transform.position = new Vector3(transform.position.x, transform.position.y, sinus);
        }
        else
        {
            transform.position = new Vector3(sinus, transform.position.y, transform.position.z);
        }
    }
}
{{</highlight>}}
Here we promote a boolean to the Unity Editor. Booleans will show up as checkboxes. So now we can select in the Editor the Cuboids we want to move along another axis. An example could look like this:
{{< figure src="/img/04MovingCuboids_ShiftingX_Appart.gif" title="Cuboids shifting on either X or Z" width="50%">}}

### Getting User Input
As Unity is in it's core a game engine one of it's core features is to do something based on User Input. Every game obviously needs this way of interaction. Unity offers a variety of Inputs. You can check if a button has pressed and get a short pulse like answer, or as for a continuous answer while a button is pressed down. These Inputs will provide you with a simple `true` or `false` answer. For more complex input methods like game controllers and joysticks you can receive their current values. You can even grab values like touches and orientation from mobile devices.\
The most basic Input we can get is "anyKey".
**Include Gif here with Button Pressed visualization**
{{<highlight c>}}
if (Input.anyKey)
{
    transform.position = new Vector3(transform.position.x, sinus,transform.position.z); 
}
{{</highlight>}}
`Input.anyKey` will return `true` as long as any Input is received. And while it's fine for our purpose, there really aren't that many practical uses to *anyKey*. Most likely you will want to check for a specific button. To ask for these, you also need to choose what kind of event you are interested in. Here are the basic methods to use:\
`GetKey()` - Returns `true` while Key is pressed.\
`GetKeyDown()` - Returns `true` the moment the Key is pressed down\
`GetKeyUp()` - Returns `true` the moment the button is released\
You will also need to specify the Key you want to check using "KeyCodes":\
{{<highlight c>}}
if (Input.GetKeyDown(KeyCode.A){
	Debug.Log("'A' was pressed");
}
{{</highlight>}}
To decide for a Key we want to check for we use "KeyCodes". You can simply provide them in the parentheses. `KeyCode.A` will check for the "A" Key on the Keyboard. `KeyCode.B` will check for the "B" Key on the keyboard and so forth. Some of these KeyCodes can be a little unintuitive. I.e. checking for `KeyCode.1` won't work. You have to specify `KeyCode.Alpha1`. "Alpha" for Alphanumerical. If you can't seem to find the key you are looking for eith the help of your IDE, check your go to search engine.
{{< figure src="/img/ConditionalCuboids_Shifting_X_Anykey.gif" title="Cuboids Shifting on Keypress" width="50%">}}

### Delta Time
Take a look back at the example above. That code works fine, but we also kind of introduced a bug into our code. The moment we press the "A" Key all our squares jump and then keep moving. A more pleasing result would be to have them starting of where we stopped them when releasing the button before. So let's think about our code. Where exactly does the movement come from?\
The movement is ingrained in our usage of time as a variable. Even worse. It is using System time, and that's really a place we can't and don't want to stop!\
We need to create our own way of advancing time. We can do that with a simple float variable.
{{<highlight c>}}
private float timePressed = 0;
{{</highlight>}}
We could go ahead ad add an arbitrary small value to our variable each frame. And we would get a seemingly smooth Animation. This would work fine as long as our machine is able to maintain a constant frame rate. By default it is limited to 60 Frames per Second as a maximum. So worst case, we would get a slower animation on slower computers. But we could disable this upper Limit and on newer computers it could easily run several times faster.\
This is actually a very common problem in 3D engines. The fix programmers came up with, is deltaTime. DeltaTime is the time that passed since the completion of the last frame. If you add the deltaTime of each frame over the time frame of a second, you should end up with more or less a second. By all means this isn't perfect, but it's as good as it gets. And as long your computer dosen't have any hiccups, this will be fine.
{{<highlight c>}}
if (Input.GetKey(KeyCode.A))
{
    timePressed += Time.deltaTime;
}
{{</highlight>}}
Now you can use timePressed instead of Time.time in your sin-Function. And the Animation should continue where it left of.
{{< figure src="/img/ConditionalCuboids_Shifting_X_AnykeyDeltaTime.gif" title="Much Better!" width="50%">}}
Here is the full code for that:\
{{<highlight c>}}
using UnityEngine;

public class ConditionalCuboidsShiftingXAKeyDeltaTime : MonoBehaviour
{
    [SerializeField]
    private float timeOffset = 0;
    [SerializeField]
    private float movementScale = 0.25f;
    [SerializeField]
    private float timePressed = 0;
    void Update()
    {
        float sinus = Mathf.Sin(timePressed + timeOffset);
        if (sinus < 0)
        {
            sinus = sinus * -1;
        }
        sinus *= movementScale;
        if (Input.GetKey(KeyCode.A))
        {
            transform.position = new Vector3(sinus - 0.25f, transform.position.y, transform.position.z);
            timePressed += Time.deltaTime;
        }

    }
}
{{</highlight>}}



### Input Manager
All of the above will pretty much only get us access to keys on the Keyboard. What about controllers and mouse input? For these Unity provides the very convenient Input Manager. It allows you to ask for named input like "Jump" or "Horizontal".  A single axis can then also be controlled by multiple buttons. If you are familiar with video games, you might have seen that you can control a car with "wasd" as well as the arrow keys. In Unity the "horizontal" input will by default react to the "left/right" keys as well as "a" and "D". It will even react to joystick input from a controller.\
These possibilities now lead to a different behavior as well. It's not enough to return a boolean for the horizontal axis, because there are more states to consider then on/off. We have to at least consider three: Left, Right and No Input. To represent this, values will typically be in between -1 and 1. Negative values corresponding to *left* and positive value corresponding to *right*.\
To see which values are read by Unity and how they are configured you need to check the Input panel in the Player Settings: "Edit ---> Player Settings ---> Input".
{{< figure src="/img/UnityInputManager.jpg" title="The Unity Input Manager" width="50%">}}
If you pop open one of the Axis you can see which buttons are mapped to the axis and the name connected with it. The name is what you would eventually use in your code to access them:
{{<highlight c>}}
float movementDirection = Input.GetAxis("Horizontal");
{{</highlight>}}
One thing to note: You are asking for the axis by name. You code editor can and will not help you here with spell-checking. If you mis-type "Horizontal", your code won't run!

### Mouse Input
So as I can't assume you have a game controller laying about, let's play with mouse Input. Mouse Input is special in a way: You have to some how deal with mouse movement speed.\
Thus the Input from "Mouse X" and "Mouse Y" will be the mouse delta, or the distance it traveled during the last frame. We could this create a variant that's based on the overall speed of our mouse!
{{< figure src="/img/ConditionalCuboids_Popping_MouseSpeed.gif" title="Movement based on MouseSpeed" width="50%">}}
{{<highlight c>}}
public class ConditionalCuboidsPoppingMouseSpeed : MonoBehaviour
{
    [SerializeField]
    private float movementSpeed = 0.01f;
    [SerializeField]
    private float movement = 0f;
    [SerializeField]
    private float bounds = .5f +.1125f;

    void Update()
    {
        movement = Input.GetAxis("Mouse X") + Input.GetAxis("Mouse Y");
        movement *= movementSpeed;
        transform.Translate(0, movement, 0);
        if (transform.position.y > bounds)
        {
            transform.position -= Vector3.up * 1.1125f;
        }
        else if(transform.position.y < -bounds)
        {
            transform.position += Vector3.up * 1.1125f;
        }
        movement = 0f;
    }
}
{{</highlight>}}



###
** TODO Mouse Input Clicking?**

### New Input System
The folks at Unity are currently working on a new Input System, that remedies some of the problems of the current one. This should most likely not concern you too much, but if you think of working on something, that needs crazy input options, you should probably take a look at that!

### Projects
#### Project 1
Your most obvious choice should be to go ahead and create more Cuboids! At least I did. \
Can you think of a way to recreate these? What would your steps be? The first two should be easy, but how would you solve the last one? Make sure to try these yourself before you peek at the code!
{{< figure src="/img/ConditionalCuboids_ShiftingXZ.gif" width="50%">}}
{{<expand>}}
Gist here
{{</expand>}}
{{< figure src="/img/ConditionalCuboids_Popping_Popping.gif" width="50%">}}
{{<expand>}}
Gist here
{{</expand>}}
{{< figure src="/img/ConditionalCuboids_BouncingBall.gif" width="50%">}}
{{<expand>}}
Gist here
{{</expand>}}

 
#### Project 2
Flyable Spaceship
{{< figure src="/img/FlyableSpaceship.gif" width="50%">}}
In this sketch we will reuse our spaceship and make it actually flyable. You should essentially know everything to realize this yourself by now. But let's go through this in theory and below I will also give you the code and the link to the final scene as an assetpack. \
So what do we need to check here? We need to check for user input for acceleration and deceleration. You could either check for hardcoded Keys our use the Input Manager and as for the vertical axis. And if there actually is user input, you will need to start translating your spaceship. \
You will have to do the same for rotation of the spaceship as well. \
In the same script you should also check for the bounds of your sketch. This will be totally up to you how you define these, I just went ahead and just moved the spaceship around in the viewport in used the value as bound, when the spaceship isn't visible anymore. \
Based on these bounds you can set the value to the exact opposite on the same axis. \
As additional things to play with you could add the flames only when the spaceship is accelerating or rotating. And you can add a planet which passes in the background over and over again. \
You could also limit the maximum speed or add more planets in the background. Feel freee to make it completely your own. \
\
Spaceship Script:
{{<expand>}}
**GIST**
{{</expand>}}
Flames Script:
{{<expand>}}
**GIST**
{{</expand>}}
Planet Script:
{{<expand>}}
**GIST**
{{</expand>}}
