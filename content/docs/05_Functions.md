# 05 - Methods
In this chapter we will talk about methods. We have been using them for a while now, without discussing them in detail. Methods are a collection of statements that do exactly one thing - or at least they should only do one thing. The `Update()` method is responsible for updating all the things you define each frame. The `Start()` method is responsible for setting things up in the beginning. <br>
Creating or “defining” our own functions will do a lot for us. For one it well help us to avoid repetition in our code. Due to this it will also help us to write way more readable code. You might have noticed, that some of the scripts have become rather confusing. Methods are a great way to bring some order back. Methods can also take in arguments they can process to either change or variate what they are doing or return to you a useful value.
{{<hint info>}}
#### Methods vs. functions
Methods are called “functions” in many other programming languages and many programmers started out in another language and still use the name function when they refer to C#. But they are the same thing and I can’t guarantee that I won’t slip up at one point and use function here or there.
{{</hint>}}

### Defining methods
To *define* a very simple method we need to define two things: a so-called “return type” and name for our method. The most basic *return type* is `void` - meaning nothing. You don’t expect to get something returned to you. That why our `Update()` and `Start()` methods use `void` as a return type. They just do their thing. Methods that typically have a return type are math operations, like a `Distance()` function. You provide two points as input and expect the distance in return. Let’s look at some examples.
{{<highlight c>}}
void TimeLogger(){
	Debug.Log(Time.time);
}
{{</highlight>}}
This code defines a function that does not return anything, but prints the current time to the console. You could then call function at any point in your code, in the same script. Calling a method is as simple as using it’s name with parentheses bu without the return type keyword. So let’s look at a whole script for this:

{{<highlight c>}}
using UnityEngine;

public class LogTime : MonoBehaviour
{
    void Update()
    {
        TimeLogger();
    }

    void TimeLogger()
    {
        Debug.Log("The current timestamp is:" + Time.time);
    }

}
{{</highlight>}}
As you can see new methods are defined at the same level as the `Start()` and `Update()` method. And you can define them *below* the line where they are used. Actually we are defining the `Start()` and `Update()` methods in each script as well. The only difference between our methods and the methods predefined by Unity is, that Unity will try to call them automatically during execution, while we have to make sure our methods a called at some point.<br>

So how can a simple `void` method help us with our code? As an example let’s go back to the “Popping” cuboids from Chapter 04:
{{< figure src="/img/ConditionalCuboids_Popping_Popping.gif" width="50%">}}

{{<highlight c>}}
public class ConditionalCuboidsPopping : MonoBehaviour
{
    [SerializeField]
    private float movementSpeed = 0.25f;
    [SerializeField]
    private float bounds = .5f;

    void Update()
    {
        transform.Translate(0, movementSpeed, 0);
        if (transform.position.y > bounds +.225f)
        {
            transform.position = Vector3.up * -bounds;
        }
    }
}
{{</highlight>}}
While our `Update()` method is still reasonable in this case, to understand what is going on, we still have to read through rather “low level” code. We can clean this up by using methods. What is the line `transform.Translate(0, movementSpeed, 0);` actually doing? It’s moving the cuboid up. So let’s create a method for it.
{{<highlight c>}}
    void MoveCuboidUp()
    {
        transform.Translate(0, movementSpeed, 0);
    }
{{</highlight>}}
Now we can replace the original line with a *call* to this function:
{{<highlight c>}}
public class ConditionalCuboidsPoppingRefactored : MonoBehaviour
{
    [SerializeField]
    private float movementSpeed = 0.25f;
    [SerializeField]
    private float bounds = .5f;

    void Update()
    {
        MoveCuboidUp();
        if (transform.position.y > bounds +.225f)
        {
            transform.position = Vector3.up * -bounds;
        }
    }

    void MoveCuboidUp()
    {
        transform.Translate(0, movementSpeed, 0);
    }

}
{{</highlight>}}
What we are doing right now is called “refactoring”. We are restructuring and often simplifying or de-cluttering our code without actually changing what it does. Whenever you feel you are done with a script you should consider if there is any useful refactoring to be done. We haven’t done it so far, because we were missing the proper tools. But doing this helps you creating a beautiful and good to work with code base.<br>
So while we are at it? What more can we do? We have a part left where we check for the position and based on that pop the cuboid back down. We could put in a method called `CheckBoundsAndPopDown`. But wait! Didn’t we establish in the beginning that methods should only do one thing? They should!<br>
So let’s split both of them. Easy things first:
{{<highlight c>}}
    void PopCuboidDown()
    {
        transform.position = Vector3.up * -bounds;
    }
{{</highlight>}}
Now all the methods we have been declaring so far just did things. But how can we simplify the *if-statement* further? It needs a boolean of `true` or `false` to evaluate. This where *return types* come in. We can make our method return either true or false like this:
{{<highlight c>}}
    bool CheckYGreaterBounds()
    {
        return transform.position.y > bounds + .225f;
    }
{{</highlight>}}
Instead of `void` we simply define the type we want to return. It’s `bool` in our case, but could be anything really. Then we need to make sure our method contains a `return` statement followed by the value we want to return. In the upper code we just rely on the evaluation of the statement to return either true or false. With his done let’s look at our `Update()` method.
{{<highlight c>}}
    void Update()
    {
        MoveCuboidUp();
        if (CheckYGreaterBounds())
        {
            PopCuboidDown();
        }
    }
{{</highlight>}}
Isn’t it a beauty? Consider coming back to this script in two weeks or a month. Checking `Update()` you know exactly what is going on in the script. You don’t have to work through each line to understand what the whole script is doing. An quite actually, why would you care how something is moving up or popping down. Or say, you need to change how the cuboid is moving up, you only need to check method `MoveCuboidUp()` and not all the code in the `Update()` method.

{{<hint info>}}
### Refactoring Tricks
Assuming you are using the “Visual Studio Community” Edition that comes bundled with Unity, you can access some a shortcut in the IDE. If you select a line or multiple lines of code you want to refactor into a new method, you can simply press “Ctrl + .”. VS Community will then as you if you want to “Extract method”. Press enter and a new method including you code will be created. Also you can now instantly input a name for the method and method as well as method call will have the same name.
{{</hint>}}

### Method Arguments
The last thing we need to concern our selves with regarding methods are parameters and arguments. Parameters allow you to “pass” information to the method. This information is then in turn called an argument. You’ll see quite a few people using both things interchangeably. <br>
A very simple definition and call could look like this:
{{<highlight c>}}
int Add(int a, int b){
	return a + b;
}
int result = Add(1, 1); // returns 2
{{</highlight>}}
To add parameters to a method we simply declare their type, integer in this case, and a name for them in the parentheses we thus far left empty. In the method itself you can use these as normal variables. These are only visible to the method and you can’t use these variables outside the context of the method.<br>
To *pass* information you simply add arguments to the function call. In this case this could be literal numbers or any variables that contain an integer. Important is, you **have** to specify all arguments. You can’t just specify a single integer in the parentheses.<br>
No you can see the method we created is rather useless, but I hope it clarified the basic idea. Let’s actually look at a more advanced example:<br>
Insert Fading/Poppig Cuboids here
While this is in essence the Popping example from before, I introduced some fading towards the bounds. Let’s first look at the beginning of the script:
{{<highlight c>}}
using UnityEngine;

public class ConditionalCuboidsFading : MonoBehaviour
{
    [SerializeField]
    private float movementSpeed = 0.25f;
    [SerializeField]
    private float bounds = .5f;
    [SerializeField]
    private Color colorToSet;

    private void Start()
    {
        colorToSet = GetComponent<Renderer>().material.color;
    }

    void Update()
    {
        MoveCuboidUp();
        if (CheckYGreaterBounds())
        {
            PopCuboidDown();
        }

        if (transform.position.y < 0)
        {
            colorToSet.a = Map(transform.position.y, -.45f, -.0f, 0, 1);
        }
        else if (transform.position.y > 0)
        {
            colorToSet.a = Map(transform.position.y, .225f, .45f, 1, 0);
        }

        GetComponent<Renderer>().material.color = colorToSet;

    }
    ...
{{</highlight>}}
So what’s different? First of all, we now need to to create a Color variable, and in `Start()` we set it to the Color our Object currently has. So we can still define the color conveniently via the Material. We need to do this because we can’t directly set the Alpha value of a color on the material itself. We can though on a variable. So the last thing in `Update()` we do, is to update the color.<br>
In between do our typical movement and also change the alpha value of our color based on position on the Y axis. `ColorToSet.a` accesses the alpha component. What do we set it to? We use a method call and pass it five values! So let’s look at the `Map()` method.<br>
{{<highlight c>}}
    float Map(float value, float oldMin, float oldMax, float newMin, float newMax)
    {
        float oldAbs = value - oldMin;
        float oldMaxAbs = oldMax - oldMin;
        float normal = oldAbs / oldMaxAbs;
        float newMaxAbs = newMax - newMin;
        float newAbs = newMaxAbs * normal;
        float clampedNew = Mathf.Clamp01(newAbs + newMin);
        return clampedNew;
    }
{{</highlight>}}
The `Map()` method takes in a float value as well as values for two ranges. With it you can transfer values from one range to the other. In our example we have a range between `0.225` for the Upper Mid Cuboid and `0.45` for the Upper Cuboid. During this range we want to fade out the cuboid. But the Alpha values range from 0 to 1. Using this method we can easily convert between them.<br>
Imagine having all this in your code each time we call the `Map()` method. And yes, we surely could shorten this code, I hope you can see we not only shortened our code, but we also made sure we didn’t repeat ourselves. If now we have a problem with this mapping, we can then easily work through this method and fixing this problem will all the problem will fix all the problems with mapping.

### Magic Numbers
In this example you see some me using actual numbers/values as parameters. I.e.:
{{<highlight c>}}
	colorToSet.a = Map(transform.position.y, -.45f, -.0f, 0, 1);
{{</highlight >}}
While the `0` and `1` are probably fine, because there is no real typical reason to change those, for the others there might be a reason. Those are “magic numbers”. Numbers in the code that magically define how something works or doesn’t. You typically should avoid them at all costs. Create a variable for them! Magic numbers can be a real pain in the a** to debug, especially if you come back to code a while later.<br>
I left them, so I could make this point. You shouldn’t!

### Colors in Unity
We have been working with colors for a while now, but it always was manually selecting them through the Unity Editor. And you will see, that this has some advantages to it. *But* setting and manipulating color has it’s value, so we will look into it! <br>
{{<hint warning>}}
Color is a complex matter on so, so many levels. This sub-chapter will discuss color on a superficial level and how you could deal with it in Unity. A *slightly* deeper discussion can be found in chapter 11. In this chapter I will assume that you, as an interested person, have some basic knowledge about basic digital color theory. If you have no idea what RGB and HSL are, check the *expand* directly below.
{{</hint>}}
{{<expand>}}
#### The most important ideas about digital color
Everything we are designing in Unity right now is supposed to be displayed on a screen. Screens, in contrast to printed imagery, emit light. As it turns out adding red, green and blue light in the correct proportions will give you white light. Every pixel on your screen consist of these three colors. We thus talk about the *additive* color. Mixing these three components together will give us a very wide range of perceptible colors to display. For example mixing Red and Green will give you Yellow. Blue and Green will result in Cyan.<br>
While this concept is very nice for computers to understand, we typically don’t talk about color in terms of a combination of red, green and blue. <br>
“The suspect wore a 50% red, 50% green and 100% blue sweater.” <br>
Yeah, we don’t do that. We say:<br>
“The suspect wore a light blue sweater.” <br>
This is why people came up with “HSL”/”HSV” or Hue, Saturation and Lightness/Value. Now we can define a Hue around the color wheel, the saturation and it’s lightness or brightness. From a programming point of view it also makes some color manipulations easier, because we can access the more “human readable” components directly. <br>
{{</expand>}}
Color is its own *type* in Unity. This means colors need to be created using the `new` Keyword. The arguments we can pass to the constructor are red, green, blue and an optional alpha value. The values you need to supply the method will be floats ranging between 0 and 1. Everything beyond 1 will simply be clamped at 1.
{{<highlight c>}}
Color myRed = new Color(1,0,0); // This would be pure red
Color myGreen = new Color(0,1,0); // This would be pure green
Color myBlue = new Color(0,0,1); // This would be pure green;
Color myTransparent = new Color(.5f, .5f, .5f, .5f); // This would be a transparent middle gray
{{</highlight>}}
{{<hint info>}}
Unity comes with some static colors as well, which you can use for convenience. `Color.black` for example could be used just to quickly define a default value.
{{</hint>}}
Given this, working with colors is pretty much straight forward. A little awkward on the other hand is assigning the colors. We need to access the Color Component on the Material Component on the Renderer Component on our object. It’s a long line of code for just a small assignment and it looks like this:
{{<highlight c>}}
GetComponent<Renderer>().material.color = new Color(1,0,0);
{{</highlight>}}
While we are now able to change the color, we can just switch it to predefined values. How about we try to create a little more flexibility? <br>
Luckily Unity provides us with some Methods to retrieve or set colors differently using the Hue, Saturation and Value approach.<br>
Setting HSV Colors works very similar to creating Colors using the RGBA approach. Instead of red, green and blue, we define values for hue, saturation and value as floats.
- {{<highlight C>}}
Color myColor = Color.HSVToRGB(0,1,1);
{{</highlight>}}
But it also yields the same reults. We can define a color. We just use other means to do so. More interesting would be to actually manipulate colors. Unity does not provide a way to do this out of the box. But we can build our own manipulation tools! <br>
{{<highlight c>}}
float h,s,v;
Color currentColor = GetComponent<Renderer>().material.color;
Color.RGBToHSV(currentColor, out h, out s, out v);
h += 0.05f;
if(h > 1){
	h - 1;
}
GetComponent<Renderer>().material.color = Color.HSVToRGB(h,s,v);
{{</highlight>}}
The code for this starts growing and will also use some syntax we haven’t seen so far and yet it is rather straight forward. First we need to declare variables for hue, saturation and value. All of them will be handled as values between 0 and 1 and thus are defined as floats. Then we create a variable for our the current color of the GameObject and retrieve it . <br>
Then we use a “static” method on the color class which we pass the current color and tell it to which variables it should assign the three HSV values.<br>
With those now assigned, we can manipulate one of those values. Here we choose Hue to shift the color around the color wheel. We also add a Condition to check if we surpass 1, if so, we subtract 1 to make sure we start on the other side of the color wheel again.<br>
Finally we construct a new Color from hue, saturation and value and assign it back to our Square.
{{< figure src="/img/MethodColorShift.gif" title="Cuboids Shifting on the X Axis" width="75%">}}
In the above example, you can see this working on button press. You can see this works relatively okay for monochromatic color schemes. You will find that this approach will fail on other color schemes. But go ahead and try it!
Here is the full code:
{{<expand>}}
{{<gist HGieselmann 6b47e6aeda78995e404c2dd7d4ddc274>}}
{{</expand>}}

### Color Math
Unity also allows for doing basic math operations between Colors. The following Code would give you magenta.
{{<highlight c>}}
Color myColor = Color.Red + Color.Blue;
{{</highlight>}}
Color math is actually just Vector Math. And Vector Math is nothing else as separating the components and dealing with red, green and blue one at a time. 

### Gradients
{{< figure src="/img/MethodFadingWithGradient.gif" title="Cuboids shifting, fading and evaluating a Gradient" width="75%">}}
Another way very pleasing way to work with colors are gradients. While you could define your Gradients through code, we will just look defining them in the editor and then evaluating them at run time. While this is little bit like shifting colors around, it will also give us more artistic control, which is always nice. <br>
To create an Gradient, we declare it as an global variable. <br>
{{<highlight c>}}
[SerializeField]
 private Gradient popGradient = new Gradient();
{{</highlight>}}
We can now create our gradient inside the Unity, by clicking on the white color bar in the editor. 
{{< figure src="/img/Gradient.jpg" title="Gradient Tool in Unity" width="75%">}}
On the “Gradient” popup window you can define the gradient by adding new colors on the bottom bar and alpha values on the top bar. In this sketch I calculated and added alpha seperatly to the mix. <br>
In code, we can then evaluate the color at a position between 0 and 1 or left and right respectively. 
{{<highlight c>}}
Color curGradientColor = popGradient.Evaluate(transform.position.y + 0.45f);

{{</highlight>}}
As you can see any value can be used to evaluate this. For my sketch the position in Y makes sense to use.
The full code for the sketch can be found here:
{{<expand>}}
{{<gist HGieselmann cfbb7a7231876dedc8d738da35cdd65c>}}
{{</expand>}}




### Project 1:<br>
The first thing i suggest you do is, go through the scripts you have written so far and refactor them. An for at least a few try not to rely on the refactoring help of your IDE. Get the concept o writing them engraved into your brain!.<br>

### Projects 2:<br>
While methods don’t actually allow is to do something utterly new, it allows is creating things that aren’t horribly tedious to do. So here are some more examples for our Cuboid: Go check them out.<br>
Add more examples here using methods
### Projects 3:<br>
Noise Walker
Low poly Example
More advanced land speeder?





- Ari Danish
- Discussion of Randomness
- animated Radomness
- recreate an image each touch
-  Suprematism
- can we implement design rules to get “non random results”

- Landspeeder with things placed through noise
- 

