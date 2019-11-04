### Classes and Object Orientation

### Don’t Panic!
When I first started out coding and asked friends what their experiences was, I heard a few times: “It’s not that bad, but I don’t get Object Orientation”. And when I first heard of it or read on it on the docs I a little bit baffled as well. But when I learned C# for the use in Unity things made “click” very fast. The thing is: We have been using Object Orientation all the time already, you just didn’t realize. Whenever we created a script, it started with the `class` Keyword after the `using` statements. We just ignored it was there. So don’t be scared, it’s actually quite simple!

### Basics of Object Orientation
The most important idea of Object Orientated Programming (OOP) is to create clean, modular code which is easy to maintain. We want to group things which fit logically together and if everyhting goes well, we never have to touch that piece of code ever again. But if we have to go back in and change it, we have a file that is as small and clean as it can be, so we can do our modifications easily. So it’s really important to understand: OOP is here to help. OOP is your friend. 

### Encapsulation
Classes are the blueprints for Objects, or the idea what the object should be like. As soon as we Instantiate the class becomes an individual object.

Let’s walk through this by example. Let’s assume we had bike manufacturing and our designer came up with a new concept for a bike. So they defined if it’s a Mountain bike or a racing bike. They also defined the colors, the customer could choose from. And of course how many gears you could have. All of this is the class, the idea of the bike. So we bring it into manufacturing - which would be our equivalent to instantiation - and out comes an object. 
An Object is an actual physical version of the bike. You can’t select the color or colors anymore, because all the specifics have been defined during Instantiation. If you need a different bike, you will have to create a new bike - a new object - from the class - the idea.
Now classes and objects can also hold functions. We could have lamps which can be turned on and of. We can break, so we don’t crash our nice new bicycle. These functions are also defined in the class, and can then be used by the object we created.
This idea of packing code together is called Encapsulation and is one of the three cornerstones of Object Oriented programming. 
Encapsulation in short: Put all your code - all it’s adjectives and all the things it can do - into one class.

Another concept is “Inheritance”. We have been using inheritance all the time as well:
`public class MovingAlbers : MonoBehaviour`
That `:` right there indicated “Inheritance”. It means our class MovingAlbers Inherits from MonoBehaviour.
Inheritance means in short means, you can base classes on other classes.
To stay in our own little bike manufacturing shop, you could have a “base class” that holds all the code, that each and every bike has to have. This could be things like name, price or color. But this also could have methods or behaviours every bike must know, like accelerating and braking.
CHECK THIS CODE!!
{{<highlight c>}}
public class bike : MonoBehaviour{
	public string name;
	public Color bikeColor;
	public float price;

	public void accelerate(float acceleration){
	// code for acceleration
}
	Public string advertise(){
	string ad = “This is our bike” + name + “. It is “ + bikeColor + “ and costs “ + price;
		Return ad;
{{</highlight>}}

TODO WE NEED AN EXAMPLE OF OBJECT CREATION AND THE FACT THAT SHIT THEN IS A TYPE HERE!!!!
FUCK WE ALSO NEED TO TALK ABOUT CONSTRUCTORS AND TYPES!

### Inheritance
But now we have different customers, with very different situations. One is just commuting a few kilometers each day. So he fancies a nice, slick singlespeed bike and will also need good lights for those winter days. The next wants to go mountain biking in the alps over the summer. He wants a versatile gearbox, but sure he has no interest in a dynamo. Those are bikes with very different purposes, but both will end up having a name, a price and a color. Both can inherit these base traits from our bike class, so we don’t need to write that code twice. So we inherit bike using `:`

{{<highlight c>}}
public class singlespeedBike : bike{
	public float maxlightBrightness = 10;
	private bool lightOn = false;

	public void switchLights(){
		// Code for switching the light on and off
	}
{{</highlight>}}

Or the code for mountain bike:
{{<highlight C>}}
public class mountainBike : bike{
	Public int numberOfGears = 21;

	public void shiftUp(){
		// Code for switching the light on and off
	}

public void shiftDown(){
		// Code for switching the light on and off
	}
{{</highlight>}}

This can be extremely helpful, as it shortens our code. If we have a problem with our gearbox code, we only have to take a look at the mountain bike class. All of the base ideas are hidden away in the base class and it also has no code, that is completely irrelevant to the functioning of the bike. This is great stuff!

### Polymorphism
Polymorphism is the idea that things can be “many-shaped”. Therefore this fancy Greek word. And this is helpful in many ways. Consider this code:
{{<highlight C>}}
private mountainBike myMountainBike = new MountainBike();
private singlespeedBike mySinglespeed = new MountainBike();
{{</highlight>}}

As you can see, once we create our bikes, they become two different types. But what if we would want to creat a List or Array of all the bikes we sold. We need to keep track of that, right?
Polymorphism to the rescue. Thanks to polymorphism we can use the base class `bike` as the class we consider to create a list of items sold.
{{<highlight c>}}
// put some example code here
{{</highlight>}}
Polymorphism also means, that we can override some of the code we wrote in the base class in the child class. This can beuseful if you have some code that you need for all your objects, but then there is this one bike, where you want to change it’s implementation. It would be really annoying to remove the code form the base class and put in each child class. And it would also be bad practice to just create a new function that does exactly the same thing.
If you look at our base class again. We have that `advertise()` function. It’s a really dull advertising, but at least it works on all our bikes, right? But when our engineers came up with the mountain bike, marketing - actually same guy as the engineer - was all over the place and wanted to have the number of gears in the advertisement as well.
So we needed to change that.

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


















