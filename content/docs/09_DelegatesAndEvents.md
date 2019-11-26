# 09 - More Language Features

In this chapter we will look at some other C# features and some loose ends we left along the way, because I didn’t want to bother you with them too early. These aren’t things you definitely need to know from the get go, but they will make you a better programmer. And as soon as you wish to tackle slightly larger projects, make sure to come back here.

### Properties
C# properties allow you to specify how other scripts can access private variables in your scripts. This comes in handy, if you want a variable to be able to read a value form outside, but don’t want to be able to set it from outside. Reigning this in is done using getter and setters. These are defined in curly brackets right after the variable name.
{{<highlight c>}}
public int myPublicInt;
public int myProperty {get; set; }
{{</highlight>}}
If you look at the code we have a public variable and a public property. These two are pretty much the same thing. But we can work with these getter and setter some more.
{{<highlight c>}}
public int myProperty {get; }
{{</highlight>}}
Now if you try to write to that variable you will run into an compiler error or won’t even be able to compile. So now any Script can read that value, but no script can change the value. You even can’t change it from within the script. But we can manage that:
{{<highlight c>}}
public int myProperty {get; private set;}
{{</highlight>}}
This will allow you to read the script from outside and manipulate it from the inside. This will allow you to protect your variables from accidentally changing them from some other script. So if you don’t need to set these variables from outside, use this method to prevent bugs. <br>
You could of course also use these to prohibit reading and only allow to write from outside. Any combination is possible. <br>
So what we have seen so far are “auto properties”. They are shorthand code for something that is usually a little longer. In Unity code you will most often see auto properties, but there are fully fledged properties as well.
{{<highlight c>}}
public string myStringProperty {     get { return myStringProperty; }     set { myStringProperty = value; } }
{{</highlight>}}
This will result in exactly the same behaviour it is just more explicit. But using this larger syntax you can also add additional functionality to your getters and setters. You can change the way you return these values. Thus you could for example check if the value you want to check is actually valid inside your context.
{{<highlight c>}}
public string myStringProperty {     get { return myStringProperty; }     set     {         if (value > 100)         {             myStringProperty = 100         }         else         {             myStringProperty = value;         }     } }
{{</highlight>}}
So you can add any kind of code into the context of getting and setting values. Obviously you shouldn’t overdo this, but the functionality is there. <br>
Again, you will mostly see me use the auto properties in Unity, which will help protect variables. But if you come across larger chunks of code that start with get or set, you will know how to interpret these.


### Delegates and Events
We discussed earlier how Objects can call functions on other objects. To pick a stupid example: I as a “Salesman” Object could personally call a customer and he could learn from me about all the wonderful things my car offers. I could invoke his “learn” function and the Data I send will be given to him directly.<br>
But what if I have a 100.000 customers. Should I make a call to all of them? While that would be a nice move, sending out a letter would be fine too, right?<br>
And that’s what Events are all about. If you have information for many, many customers or classes, you just send them out and anyone who subscribed to the event will get notified about it.<br>
So what are delegates and what are Events?<br>
The event is the letter you want to send out. The delegate is an agreement between you and the customer how the event is supposed to look like. Say the letterbox. Your customers expect letters in there, but if you suddenly start sending packages, then they can’t be received because they don’t fit the letterbox.<br>
In code this mean the delegate is an agreement between sender and receiver what kind of data is send with the event.

So this system in itself is useful, but it also comes with some advantages for our code. Once this is set up, any class can subscribe to the event, without us ever changing the code in the class that is invoking the event. So this helps us stay flexible in our code.<br>
In larger projects this can also lead to shorter compilation times, which is always a plus!

### How to setup events?<br>
Implementing delegates and Events into our projects consists of five essential steps:<br>
1. Create the agreement about the event a.k.a. the delegate<br>
2. Create the event based on that delegate<br>
3. Create the event handler to receive the event<br>
4. Subscribe to the event<br>
5. Raise/Call the event<br>

As an first very simple example, we will a have a sphere which is slowly shrinking, but once you press a button it will be set to it’s initial Size again. Arguably you could solve this without Events, but bear with me.

So we need to create two Scripts. One for the sender of the event and one for the receiver. So let’s just call them Sender and Receiver. So first thing we then need to do is create the agreement or delegate. The delegate belongs into the Sender class.
{{<highlight c>}}
public class Sender : MonoBehaviour
{
    public delegate void ButtonPressedEventHandler();
    void Start(){...}
{{</highlight>}}
The delegate needs to be public so it can be seen by all the other classes. The `delegate` keyword tells C# that this actually IS a delegate. Now the `void` is up to us. Essentially we define a function, and if it is supposed to return a value, it can. But we don’t need it, so we’ll go with `void`. Lastly we define a name for the delegate. Naming follows the same ideas as for methods, but we will use this delegate for handling Events, thus suffixing `EventHandler` is good practice. This really just defines how the functions working with this need to look like.
{{<expand>}}
### Delegates under the hood
Delegates under the hood just enable you to store references to methods in variables. Then you can assign methods to that delegate and later call that delegate like a function. You can even add multiple functions to the delegate using `+=` and later call all of them at once. See Microsofts definition here: https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/delegates/
{{</expand>}}

Next we create the event itself. 
{{<highlight c>}}
 public event ButtonPressedEventHandler buttonPressed;
{{</highlight>}}
It is also public, as it needs to be seen by the subscribers. Followed by the `event` Keyword. The type is the name of the Delegate we just created and finally we give it a name.

Now lt’s switch over to the recieving Script. Here we first need to create a function that is called when the event is raised. What’s really important here is that this function matches the definition of the delegate we created!
{{<highlight c>}}
void OnButtonPressed(){
        transform.localScale = Vector3.one * 5;
    }
{{</highlight>}}
As you can see, the delegate we created has a return-type of void and takes no arguments. The same goes for our `OnButtonPressed` function. So that’s easy. On to step four!

Now our receiver needs to subscribe to the event.
{{<highlight c>}}
public GameObject sender;
    
    void OnEnable()
    {
        sender.GetComponent<Sender>().buttonPressed += OnButtonPressed;
    }
{{</highlight>}}
The first thing we do here is create a reference to the Sender Object as we have done many times before. So we will need to connect these in the Unity Editor!<br>
Then in the `OnEnable()` method we get the sender component and look for the `buttonPressed` event. We then add the `OnButtonPressed` method to the event a.k.a subscribe it to the event. Form now on, when ever the Event is raised, the `OnButtonPressed()` method is called.<br>
{{<expand>}}
### OnEnable()
What is OnEnable() and why do we use this? OnEnable() is similar to Start() and Update() one of those predefined functions inside Unity and they run in specific order. Thus there are recommendations on what kind of things you want to call when. If you want to go down the rabbit hole:
https://docs.unity3d.com/Manual/ExecutionOrder.html
{{</expand>}}

So how to raise the event?
We of course need to do this back in our sender Script. And all we need to do is call the event like any other function we call:
{{<highlight c>}}
	buttonPressed();
{{</highlight>}}
So far so good. But let’s embed it into our code.
{{<highlight c>}}
void Update()
    {
        if(Input.GetKeyDown(KeyCode.A)){
            if (buttonPressed != null){
                buttonPressed();
            }
        }
    }
{{</highlight>}}
 In `Update()` we check for someone pressing the “A” key. Then we check if `buttonPressed` is not Null. If this returns `Null` it means button pressed has no subscribers and then there is no need to actually raise the event. Worse! If you don’t check for this, it will actually throw an Null reference exception at runtime!<br>
But if it’s not null, this will actually run just fine!<br>
This is awesome. But let’s clarify a bit more why this is awesome. Now we can add as many functions to this event as we want! Let’s just create a function to randomly color our sphere:
{{<highlight c>}}
void OnButtonPressedColor(){
 
        this.GetComponent<Renderer>().material.color = new Color(Random.Range(0f,1f), Random.Range(0f,1f),Random.Range(0f,1f));
    }
{{</highlight>}}
We can then just subscribe this to the event as well:
{{<highlight c>}}
sender.GetComponent<Sender>().buttonPressed += OnButtonPressedColor;
{{</highlight>}}
Now we didn’t have to change anything in the sender class. The sender class doesn’t care or even know about what we did here! You could now easily add new classes that also implement this and would never again need to change the sender class.

### Unsubscribing from events
Now one thing that would be considered good practice is unsubscribing once your object get’s disabled or destroyed. That is as simple as subscribing actually. Just use `-=` in `OnDisable()`.
{{<highlight c>}}
 void OnDisable(){
        sender.GetComponent<Sender>().buttonPressed -= OnButtonPressed;
        sender.GetComponent<Sender>().buttonPressed -= OnButtonPressedColor;
    }
{{</highlight>}}

#### Static events
While all of this is fine, it’s also a lot of stuff to take care of. So let’s look into simplifications, now that you know the full version of it. The easiest simplification is to make your event `static`.<br>
This allows us to not create an object Reference in the receiver first. You can just subscribe to the event calling the class like this:
{{<highlight c>}}
Sender.buttonPressed += OnButtonPressed;
{{</highlight>}}

#### Actions
We can even go further and reduce the delegate creation and event creation into one line. To do this we first need to import the System namespace. `using System;`<br>
Then we need to change the way we declare our delegate:
{{<highlight c>}}
public static Action buttonPressed;
{{</highlight>}}
This will now be enough and an we can subscribe directly to this Action. In case you need to add parameters to your events, the syntax changes and you need to provide them in `<>` braces after the `Action` keyword. The following code would expect an integer and float as input values.
{{<highlight c>}}
public static Action<int, float> buttonPressed;
{{</highlight>}}
And thus you need to supply values as arguments when calling the function!<br>
As you can see Actions can simplify delegates and events a lot. But I wanted to make sure to show you the whole process, so you are able to read code that uses the extended method.

TODO
- Example Multiple Classes
- Example with a return type
- Example with Func instead of Action





### Pojects
- Death Events and delegates
- Cuboids to interact with
- 