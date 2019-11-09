# 08 - Classes and Object Oriented Programming
### Don’t Panic!
Friends of mine who studied engineering used to complain about the idea of Object Orientation and that it is kind of hard to grasp. I can’t say anything about the programming language or the environment they had  to learn in, but inside Unity this is actually rather simple. The thing is: We have been using Object Orientation all the time, you just didn’t realize it. Whenever we created a script, it started with the `class` Keyword. We just ignored it was there. This keyword means we created a class each time. And classes become objects once they manifest themselves. This means: Don’t panic. We will just pull some pieces together in this chapter.

### Basics of Object Orientation
The most important idea of Object Orientated Programming (OOP) is to create clean, modular code which is easy to maintain. We group things which fit logically together and if everything goes well, we never have to touch that piece of code ever again. But if we have to go back in and change it, we have a file that is as small and clean as it can be, thus we can do our modifications easily. It’s really important to understand: OOP is here to help.

### Encapsulation
Classes are the blueprints for Objects, or the idea what the object should be like. As soon as we *Instantiate* it, the class becomes an object.

Let’s walk through this by example. Let’s assume we had bike manufacturing and our designer came up with a new concept for a bike. So they defined if it’s a Mountain bike or a racing bike. They also defined the colors, the customer could choose from. And of course how many gears you could have. All of this is the class, the idea of the bike. So we bring it into manufacturing - which would be our equivalent to instantiation - and out comes an object.
An Object is the actual version of the bike. You can’t select the color or colors anymore, because all the specifics have been defined during Instantiation. If you need a different bike, you will have to create a new bike - a new object - from the class.
Now classes can also define behaviour or methods. We probably want to be able to accelerate. We should also be able to brake, so we don’t crash our nice new bicycle. We might even have some lights on there, so we can see at night. These methods are also defined in the class, and can then be used by the object we created.
This idea of packing code together is called “Encapsulation” and is one of the three cornerstones of Object Oriented programming. 
Encapsulation in short: Put all your code that logically belongs to one object - all it’s properties and all the methods - into one class. An example bike class could look like this, and you will see, this is exactly the same we did all the time.
{{<highlight c>}}
using UnityEngine;  public class Bike : MonoBehaviour {     public Color bikeColor = new Color(1,1,1);     public int price = 499;      private float currentSpeed = 0f;     private float acceleration = .1f;     private float deceleration = .25f;     private float maxSpeed = 10;      void Update()     {         HandleInput();         Move();     }      private void HandleInput()     {         if (Input.GetKey(KeyCode.A))         {             Accelerate();         }else if (Input.GetKey(KeyCode.S))         {             Brake();         }     }      void Accelerate()     {         currentSpeed += acceleration * Time.deltaTime;         if (currentSpeed > maxSpeed)         {             currentSpeed = maxSpeed;         }     }      void Brake()     {         currentSpeed -= deceleration * Time.deltaTime;         if (currentSpeed < 0)         {             currentSpeed = 0;         }     }      void Move()     {         transform.Translate(Vector3.forward * currentSpeed);     } }

{{</highlight>}}

### Inheritance
Another concept is “Inheritance”. We have been using inheritance all the time as well:
`public class MovingCuboid : MonoBehaviour`
That `:` right there indicated “Inheritance”. It means our class MovingCuboid Inherits from MonoBehaviour.
Inheritance means in short means, you can base classes on other classes.
To stay in our own little bike manufacturing shop, you could have a “base class” that holds all the code, that each and every bike has to have. This could be things like name, price or color. But this also could have methods or behaviors every bike must know, like accelerating and braking. The class we have seen previously could be used as our base class.
But now we have different customers, with very different requirements. One is just commuting a few kilometers each day. So he fancies a nice, slick single speed bike and will also need good lights for those winter days. The next wants to go mountain biking in the alps over the summer. He wants a versatile gearbox, but sure he has no interest in a dynamo. Those are bikes with very different purposes, but both will end up having a name, a price and a color. Both can inherit these base traits from our bike class, so we don’t need to write that code twice. So we inherit bike using `:`

{{<highlight c>}}
// This code is more schematic, and not an actual implementation
public class SingleSpeedBike : Bike {     public float maxlightBrightness = 10;     private bool lightOn = false;      public void switchLights()     {         if (lightOn)         {             lightOn = false;         }         else         {             lightOn = true;         }     } }

{{</highlight>}}

This can be extremely helpful, as it shortens our code. It also helps us to avoid writing code all over again. It makes things easier and faster to write and to debug.
As you can see, on this one, we don’t inherit from MonoBehaviour. We already did so in the base class, thus we don’t have to on the SingleSpeedBike class.

### Polymorphism
Polymorphism is the idea that things can be “many-shaped”. Therefore this fancy Greek word. And this is helpful in many ways. Consider this code:
{{<highlight C>}}
private mountainBike myMountainBike = new MountainBike();
private singleSpeedBike mySingleSpeed = new MountainBike();
{{</highlight>}}

As you can see, once we create our bikes, they become two different types. But what if we would want to create a List or Array of all the bikes we sold. We need to be able to keep track of that, right?
Polymorphism to the rescue. Thanks to polymorphism we can use the base class `bike` as the class we consider to create a list of items sold.
{{<highlight c>}}
	List<Bike> MyBikes = new List<Bike>();
	MyBikes.Add(myMountainBike);
	MyBikes.Add(mySingleSpeed);
{{</highlight>}}

Polymorphism also means, that we can override some of the code we wrote in the base class in the child class. This can be useful if you have some code that you need for all your objects, but then there is this one bike, where you want to change it’s implementation. It would be really annoying to remove the code form the base class and put in each child class. And it would also be bad practice to just create a new function that does exactly the same thing.
If you look at our base class again. We have that `Acclerate()` method. If we were to create a mountainBike with some kind of gearbox, we would need be able change the we accelerate right? Somehow our gears need to have an effect on acceleration.

{{<highlight C>}}
public class mountainBike : bike{
	Public int numberOfGears = 21;

	public void shiftUp(){
		// Code for switching the light on and off
	}

public void shiftDown(){
		// Code for switching the light on and off
	}

public override string advertise(){
	string ad = “This is our bike” + name + “. It is “ + bikeColor + “ and costs “ + price + “It also has “ + numberOfGears “ gears!!”;
		Return ad;
{{</highlight>}}

In our child class mountainBike we declared the advertise function again, but added the keyword `override` in front. The moment we instantiate our mountainBike the advertise function in the base class is overriden and we can now finally advertise our fancy gearbox!


### Constructors
Add these for completionists sake



