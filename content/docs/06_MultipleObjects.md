# 06 - Multiple Objects
### Multiple Object Workflow
If you followed along with some of the examples, you probably realized we do a lot of manual labor. We deal with the Unity Editor a lot. We apply all the new scripts manually to each Cuboid. Then again programming is a lazy mans art. The less manual labor we have to do, the better. <br>
With the concepts introduced in this chapter, we will be able handle lots and lots of objects simultaneously. Hence it will also allow us to create more complex sketches. <br>
To do this conveniently in Unity we need to look at three Concepts: <br>
1. Prefabs and Instantiation <br>
2. Arrays and/or Lists <br>
3. Loops <br>
In short, we will create objects through Instantiation. We will the use Arrays and Lists to keep track of them and loops to iterate over them. <br>
What’s even better is, it opens up a lot of creative possibilities and ideas to talk about! <br>
We will also look at interaction between multiple scripts. Finally keywords like `private` and `public` will hopefully make more sense.

### Prefabs and Instantiation
Instantiation is the process of creating or “instantiating” objects from a script and it is tightly intertwined with the Concept of Prefabs. Prefabs are “prefabricated” Objects we can create through the project view. In most cases these prefabs are the object we want to instantiate through code at runtime.
Creating Prefabs is surprisingly simple. Any object you have in your scene can be turned into a prefab. All you have to do is drag an item from the hierarchy into the project view. Go ahead and create an cuboid prefab from any of your sketches.
{{< figure src="/img/CreatePrefab.gif" title="Creating a Prefab via Drag and Drop" width="100%">}}
The tiny cube in front of the object turns blue if Unity knows about this object as an Prefab. It’s often advisable to create a specific folder for all your prefabs. <br>
Unity will keep all of the components currently attached to the prefab. Any behaviour we have added to a prefab will be there once we create an instance of it. For example a cuboid with a script that makes it move automatically attached to it, will lead to this exact same movement the moment you Instantiate it at runtime. <br>
Once you have created a prefab from a GameObject you can go ahead and delete it from the hierarchy, if you don’t need it there anymore.


### Instantiation
With an prefab ready, we will need to create a script to actually handle the creation/instantiation of all our cuboids. Because scripts in Unity can’t exists in empty space, we need to create a GameObject to hold our script. Technically any object would work, yet an “Empty Object” would of course be the ideal choice. *Empties* only consist of a transform component and thus have no visual representation in the scene. Rename your Empty to something like “ScriptHolder” or “Manager”. <br>
First we have to find a way to grab hold of our prefabricated cuboid. In Unity all Objects (that inherit from Monobehaviour - we’ll discuss this in Chapter 08) can be referenced as GameObject. So let’s create a variable of type `GameObject` for our cuboid.
{{<highlight c>}}
[SerializeField]
private GameObject cuboidPrefab;
{{</highlight>}}
Now go back to Unity and check the Inspector. You will see a field named cuboidPrefab. You can now drag and drop the prefab you created from the Project view into the field on the inspector.
{{< figure src="/img/DragPrefab.gif" title="Connecting a prefab to your script" width="1000%">}}
Now the script *knows* about the prefab. You might argue, that this process feels a little strange, and I am with you. I tend to forget this step and run into an error. But you’ll get used to it! <br>
Next we need to actually create an actual instance at runtime:
{{<highlight c>}}
Instantiate(cuboidPrefab, Vector3.zero, Quaternion.identity);
{{</highlight>}}
The `Instantiate()` Method takes three arguments: <br>
1. The Object we want to Instantiate <br>
2. A Vector3 as Position in Space <br>
3. Rotation passed as a Quaternion. <br>
For now, just use `Quaternion.identity;`. Quaternions are scary things and `Quaternion.identity` will place them in the exact state you created the Prefab in, so that’s very likely correct anyway. <br>
If you run your scene now, you should have one Cuboid moving around, based on the script you had attached to it, when creating the prefab. <br>
Go ahead and duplicate that line and run the code again. It should give you two cuboids and yet you should only see one. Both are created in exactly the same space and size. But you should be able to see two of them in the hierarchy. You could go ahead and change the position at which you instantiate the object, or we could position it after instantiation. <br>
To move it afterwards, we need to find a way to access a GameObject after instantiation. To do that we can just assign the created Object to variable the moment we create it:
{{<highlight c>}}
	var cuboid = Instantiate(cuboidPrefab, Vector3.back, Quaternion.identity);
{{</highlight>}}
{{<hint info>}}
#### the ‘var’ Keyword
You might stumbled across the ‘var’ Keyword here. You will see code that never uses ‘var’ and code which makes a lot use of it. Generally speaking you should only use it when through the context it is unmistakeable which Type is referenced. This is mostly true for “Object stuff”. To keep it simple for now. As an Example:
`GameObject myGameOject = new GameObject();`<br>
This would create a new empty GameObject. But the line of code isn’t a beauty, is it? That’s where var comes in:<br>
`var myGameObject = new GameObject();`<br>
Don’t worry about it too much for now. This will become second nature over time.
{{</hint>}}
Now we have a variable for our cuboid. This variable allows us to access the the cuboid and all the properties of it, that are actually public.
{{<highlight c>}}
cuboid.transform.position = new Vector3(0,0,0);
{{</highlight>}}
This is the first time `private` and `public` actually become relevant for us in a scripting sense. Try accessing some of the variables we created on the script. You will probably not be able to access them, as we made almost all of them private. The transform component on the other hand is public by default. <br>
So to actually recreate our Homage to the cuboid we would need to do this over and over again and then adjusting things and... nah...  We are not going to do that! As I said before, we want to simplify things! Let’s head into loops!

### For Loops
To be able to handle many Objects (or any kind repeating process) programming languages offer “loops”. Loops are blocks of code that are executed over and over again until a certain condition is met. Maybe the most common implementation of a loop is the “for loop”. <br>
For Loops in C# need three things to work: Initializer, condition and iterator. To think of an example, assume having a jar of cookies and you are allowed to eat 50 cookies in a week. So you need to make sure how many you have eaten so far. So you take a piece of paper and start a tally sheet. This tally sheet is your initializer. The Initializer is just creating a variable to keep track of a number. <br>
Then each time you want a cookie you check whether you are still allowed to eat a cookie or if you already had 50. That’s the condition. Once you have eaten the cookie you add one to your tally sheet. That’s done using the iterator. <br>
Actually eating the cookie is the code in the loop. That’s wrapped in curly braces again.
{{<highlight c>}}
for (int i = 0; i < 5; i++)
{
    Debug.Log(i);
}
{{</highlight>}}
A *for loop* starts with the `for` Keyword followed by parentheses. The first thing is our tally list / Initializer. It works exactly like creating any other variable in Unity, but you *have* to initialize it. What’s also to note is: Counting in computer science almost always starts with 0. Thus we will start with `int i = 0`! The three parts of a loop are separated by a semicolon. Next up is the condition. Conditions in for loops check if your counter is higher or lower then a certain threshold and if it evaluates to false the loop will stop. Finally, the iterator determines by which value to increase or decrease your tally list. In this case the `i++` just means the variable `i` will be increased by one after each iteration. You could also put `i+1`. Actually you can advance your initializer in any step size: `i + 2`, `i + 100` or even `i - 1`. They all work fine. <br>
In curly braces follows the code to run. In the above counter we just print the value of our counter `i` to the console.

**### Create example with for loop here**

### Arrays
That’s it for the theory, lets put this into practice. Earlier, when were discussing Instantiation, we said we need a variable to create a reference to our objects. But creating five variables, each to hold a cuboid would be a pain. That’s why we also introduce Arrays. Arrays hold many things of one same type. A list in essence, except that they aren’t really list because list exist as well and... well... this is messed up. They are seperate things and we’ll look at Lists a little later.<br>
Anyway... Arrays hold things of the same *type*. Like *float* or *integer*. Or *GameObject*! Creating Arrays is simple. You create them like any variable, but add `[]` after the type.
{{<highlight c>}}
private GameObject[] myGameObjectArray;
{{</highlight>}}
Now we have created the Array, but we didn’t initialize it and thus can’t use it. The thing with Arrays is, that they always have a fixed length. So in the moment you *initialize* the array, you need to specify how many items you want to store in your list. For our cuboid example, it’s as simple as this:
{{<highlight c>}}
private GameObject[] cuboids = new GameObject[5];
{{</highlight>}}
We have to specify the length of the Array again in brackets after the type. But what if you wanted to do this based on a variable? You can create the variable for this on global scope and then initialize the array in `Start()` or `Update()`.
{{<highlight c>}}
    private GameObject[] cuboids
    public int arraySize = 5;
    // Start is called before the first frame update
    void Start()
    {
        cuboids = GameObject[arraySize];
    }
{{</highlight>}}
This construct gives you some flexibility, but you can’t change the actual length of the array. <br>
To access things inside an array we use the bracket notation again.
{{<highlight c>}}
	Debug.Log(cuboids[0]);
{{</highlight>}}
This would print the first object in the Array to the console. As we said earlier, counting always starts with `0`! Thus `myGameObject[1]` would give you the second entry and so forth. <br>
So now let’s look at actually making use of this:
{{<highlight c>}}
    public GameObject cuboidPrefab;
    private GameObject[] cuboids = new GameObject[5];
    void Start()
    {
        for(int i = 0; i < arraySize; i++)
        {
            myGameObjects[i] = Instantiate(cuboidPrefab, Vector3.up * i, Quaternion.identity);
        }
    }
{{</highlight>}}
This code incorporates everything we have covered so far. We first create a variable `myPrefab`. We then create a variable for an array of GameObjects and also create a variable for the size of the array. In `Start()` method we then initialize the array to the size of the variable. Henceforth it can hold five objects right now. But at the moment all slots are empty. <br>
Next we need to create a *for loop* and it’s condition is that our initializer is smaller than our `arraySize` variable. During the loop w-e access each slot of the list by it’s number, using the iterator. We also use the iterator as an multiplier for the position, thus shifting each object up by one.
{{< figure src="/img/MultiShiftingX.gif" title="Multiple Cubes Shifting" width="75%">}}
As you can see, the cuboids now move happily along in sync. But they all still have same color and all of them have the exact same offset. <br>

### Script Communication
So what if we want to change the color of these? We need to find a way to access the Color component of the objects. And we have done this before in Chapter 5. But this time we access the GameObject in our array first.
{{<highlight c>}}
for(int i = 0; i < cuboids.Length; i++) {     cuboids[i] = Instantiate(cuboidPrefab, Vector3.up * (stepSize * i), Quaternion.identity);     cuboids[i].GetComponent<Renderer>().material.color = colors[i];
}
{{</highlight>}}
As you can see, we are able to access components on other objects, if we stored a reference to the object beforehand. Here we instantiate the object, and store it directly in a slot in our array. We can then directly use this stored reference on the next line to grab the Renderer on that object and set its color. <br>
But how about the time offset? <br>
This works exactly the same. Every script we create an add to an object is a component like every other component Unity provides. Instead of *Renderer* we can now as for the Script we had attached to the cuboid when we created the prefab. This is what it looks like for me:
{{<highlight c>}}
float timeOffset = 0.25f;

for(int i = 0; i < cuboids.Length; i++)
{
    cuboids[i] = Instantiate(cuboidPrefab, Vector3.up * (stepSize * i), Quaternion.identity);
    cuboids[i].GetComponent<Renderer>().material.color = colors[i];
    cuboids[i].GetComponent<CuboidShiftingX>().timeOffset = timeOffset * i;
}
{{</highlight>}}
The script I had attached to it, was obviously called “CuboidShiftingX”. In this component I access the 
timeOffset variable and set it. 
{{<hint danger>}}
Now YOU should run into an error here. Thus far, we have all our variables set to `private`. This will prevent you from accessing and setting this value from outside. To make this possible, go into the script you have attached to the prefab and change the value you want to change to `public`. Now Unity will grant you access to this variable.
{{</hint>}}
As you can also see I multiply this with another `timeOffset` I created in the first line. This will just shift it a little for each cube and not offset it by a whole second.
This is also to show explicitly, that you can have the same variable name on different scripts. They are completly different things!
{{< figure src="/img/MultiShiftingXFull.gif" title="Multiple Cubes Shifting" width="75%">}}
If you feel that this syntax is complicated, take the time an rebuild some of the sketches we build so far. Also feel free to play around with the number of cuboids you create this way. Make sure to feel comfortable with the idea of Arrays and the usage of `i` in this context. Arrays are important and we will leverage their power a lot from now on.

**Add in  examples with Scripts applied to prefabs**


### A single script
All of the examples above use the idea of having the behavior attached to the prefab itself. To make this even more flexible, we could add our behavior at run time as well. <br>

**Replace by Gist**
{{<highlight c>}}
using UnityEngine;

public class Tests : MonoBehaviour
{
    [Serialize Field]
    private GameObject myPrefab;
    private GameObject[] myGameObjects;
    [SerializeField]
    private int arraySize = 5;
    // Start is called before the first frame update
    void Start()
    {
        myGameObjects = new GameObject[arraySize];

        for(int i = 0; i < arraySize; i++)
        {
            myGameObjects[i] = Instantiate(myPrefab, Vector3.up * i, Quaternion.identity);
            myGameObjects[i].AddComponent<Cuboid_MovingUp>();
        }
    }
}
{{</highlight>}}
Using `AddComponent<>()` we can add any script or component Unity offers. Any script you have created in your project is available as a component and can be added this way. So this script could handle all of your variants. All you needed to do was to change the component you add. <br>
I hope you can see how much easier this approach is. All you need is a Prefab for your cube without any behavior. Everything else can be managed from this script. 
Now you *could* go ahead and even manage the behavior through this script. But that down the line, that really becomes messy. As we have the option to work in different scripts and classes, we should make use of this. Robert C. Martin created the term “Single responsibility principal” for this. And it is a good idea to honor this principle.

### Half time!
Just as a head up. Once you have reached this point of the chapter you have reached half time. And even better. Everything that follows is pretty much just more of the same. Just a little different. So if you are good with everything you’ve read so far, the rest will be a piece of cake! <br>
First we will cover variants of the “for loop” and then we will look into Lists - essentially a variant of the Array. We will finish this chapter with a look at multi-dimensional arrays.

### For-each Loops
As I mentioned at the beginning of the chapter, C# offers different variants of loops. They were mostly created to make some common problems more convenient. “For-each” loops work similar to “for” loops, except you don’t need have to bother with the iterator and the initializer. *For-each* loops iterate over every item in the list and don’t need an iterator. <br>
Their syntax is very straight forward as well.
{{<highlight c>}}
private GameObject[] cuboidList = new GameObject[5];
foreach (GameObject currentGameObject in cuboidList) {
	CurrentGameObject = Instantiate(cuboidPrefab, Vector3.zero, Quaternion.identity); 	currentGameObject.GetComponent<Renderer>().material.color = Color.Black; }

{{</highlight>}}

You start with the `foreach` Keyword. In parentheses you follow that up with the type of object you want to iterate over. We have a list of GameObjects, so we iterate over those. Next we create a name, which allows us to actually access the current GameObject in each iteration. This is what `cuboidList[i]` would be in “for” loops. Lastly we just specify the array or list we want to iterate over. We just need to add the little word `in`.
All of this actually reads almost like English. On the downside, we are not automatically handed an iterator. Thus if we can not position our cuboids based on that iterator. <br>
Here you can see, why there are different kinds of loops. *For-each* loops are great if you just want to search for an item in a list. Or you want to apply a certain mechanic to all items in the list. *But* if you want to do this based on the position of the object *in* the list, the good old *for* loop is better suited to handle this.

### While Loops
The last to loops have become more uncommon over time, yet they too still have their uses! <br>
“While” loops are the most basic type of loop and essentially just run as long as a condition stays true. Think of the Update function. It loops each frame, but of course has no counter to finish after a certain amount of Frames. That would be silly. Essentially it will loop as long as the game is running. The syntax for while loops is very basic:
{{<highlight c>}}
while(true){
	//Code to run
}
{{</highlight>}}
All you need is the `while` keyword followed by the condition in parentheses. The condition has to evaluate to a boolean. In the above example I set this to `true`. That would be an infinite loop. `true` can never just become false. So this will run forever and will freeze your program. So you have to be careful how you construct your conditions with while loops.
{{<highlight c>}}
While(1 > 0){
	//Code to run
}
{{</highlight>}}
This again would be an infinite loop, because `1 > 0` will always equate to true. 
{{<highlight c>}}
int i = 0;
while( i < 10){
	i++;
	//Code to run each iteration
}
{{</highlight>}}
This code would actually work just fine. It’s essentially recreating the for loop. <br>
But you could of course use this in cases, when you want to base the iteration on some kind of outside variable. Just make sure to be able to make the condition can become false based on operations inside the while loop.

**Build a Sektch with While loops**


### Do-While Loops
There is one last kind of loop which C# offers. The “do-while” loop. As the name suggests it’s very tightly entangled with the while loop. It also works on a condition you have to falsify from inside the loop, but the evaluation of the condition is done after the first iteration of the loop. This guarantees that the code inside the loop is run at least once. This is a rather special case, but can be useful in some situations.
{{<highlight c>}}
int i = 0;
do 
{
    Debug.Log(i);
    i++;
} while (i < 5);
{{</highlight>}}

**Example Project here?? ??!!**


### Lists
While you could say that arrays are essentially *Lists* in C# they are two slightly different things. And most of the differences matter more to the advanced programmer: Arrays have a fixed size and can thus be placed as one continuous block in memory, while Lists are dynamic and are able to resize. This leads to both of them having advantages in one area over the other. And a good rule of thumb is: If you can get away with an Array of a fixed size, use it! At least in Unity.
{{<expand>}}
{{<hint info>}}
### More general C# 
C# as a language is used for widely different things and many of these don’t require to update at constant 60 FPS. Thus you will see people advise to use Lists over Arrays in most cases. Lists come with more features out of the box and thus are more convenient to use. When performance is not your main concern, that is absolutely correct. If you deal with small scenes I’d say it is also fair to use lists. Once you have to deal with lots and lots of objects and are concerned about performance, definitely use arrays.
{{</hint>}}
{{</expand>}}
With technicalities out of the way, let’s look at recreating one of our sketches we built with arrays using lists.
{{<highlight c>}}
private List<GameObject> cuboids = new List<GameObject>();
{{</highlight>}}
You create Lists using the `List` Keyword followed by a type `T` in angle brackets and the name you want to give to your List. You will also need to create it using the `new` keyword. Mind the parentheses at the end! <br>
To add objects to your List during runtime you can simply use the `Add()` method provided by lists.
{{<highlight c>}}
	cuboids.Add(myGameObject));
{{</highlight>}}
An example using Lists and the behavior directly attached to the prefab, would look like this:
**REPLACE BY GIST**

{{<highlight c>}}
using System.Collections.Generic;
using UnityEngine;

public class MultiCuboidsLists : MonoBehaviour
{
    public GameObject cuboidPrefab;
    public float cuboidDistance = 0.225f;
    private List<GameObject> cuboids = new List<GameObject>();
 
    void Start()
    {
        for (int i = 0; i < 5; i++){
            cuboids.Add(Instantiate(cuboidPrefab, Vector3.up * (cuboidDistance * i), Quaternion.identity));
        }
    }
}
{{</highlight>}}

Add Sketch
Accessing items in a list is actually done in the same way Arrays access items: Using bracket notation.
{{<highlight c>}}
    void Update(){
        for (int i = 0; i < 5; i++)
        {
            Vector3 position = Vector3.left *  Mathf.Sin(Time.time * cuboidDistance * i);
            cuboids[i].transform.position = position;
        }
    }
{{</highlight>}}
As you can see Lists and Arrays are similar. But take a look at all the methods Lists supply. You can not only `Add()` or `Remove()` elements from them. There are many useful things, like `Sort()`, `Clear()` and even `ToArray()` methods. These methods and their flexibility regarding length are the main features you should look out for, when deciding between lists and arrays.<br>
I suggest you play around with both options to get a feel for them.

### Multi-Dimensional Arrays
So what if you wanted to position your objects not just in a single axis, but in multiple axis? Now you could probably come up with some way to handle this using ifs or modulos. Or you would just use multidimensional arrays. They work and behave just like one-dimensional arrays, but you will have to nest your loops. You can create as many dimensions as you want, but we will only look at two and three dimensions.
{{<highlight c>}}
private GameObject[,] cuboidArray = new GameObject[5, 5];
{{</highlight>}}
This code would create a two-dimensional Array with an array Length of 5 in each dimension. Now most likely you want to assign GameObjects to your Array using an *for loop*. What you will need to do now is nest two for loops into each other, with a different iterator for each loop.
**
Convert to Gist?
Replace by script that values single responsibility**
{{<highlight c>}}
public int arraySize = 5;
public float offset = 1.5f;

void Start()
    {
for (int i = 0; i < arraySize; i++)
        {
            for (int j = 0; j < arraySize; j++)
            {
                Vector3 cuboidPlacement = new Vector3(i * offset, 0, j * offset);
                cuboidArray[i,j] = Instantiate(cuboidPrefab, cuboidPlacement, Quaternion.identity);
            }
        }
}
{{</highlight>}}
As you can see, all we need to do is use `i` and `j` in our array accessor. To spread out the cuboids, we use `i` on the x axis for positioning and `j` for the z axis. The offset will spread them out with some space between them.<br>
{{< figure src="/img/MultiDimensionRotation.gif" title="Multiple Cubes Shifting" width="75%">}}
{{<hint danger>}}
Please, be careful with these though! It is really easy to underestimate how many objects you create by just typing in some numbers. An 2D array of 10x10 is a 100 cuboids. An 3D array of 10x10x10 is 1000. Put in 100 and suddenly you expect Unity to create a million cuboids! <br>
Now depending on your background, you might think: “A million squares isn’t that much...”. Think of the way we handle these right now. There is absolutely no optimization done. Each of them is considered equal with all of its components. Thus... Be careful, save your work early and often before you pump up those numbers. (And now go ahead and crash Unity, as I know you will...)
{{</hint>}}

All of this works exactly the same using three dimensions:

**Replace by Gists!
Replace by script that values single responsibility**

{{<highlight c>}}
using UnityEngine;
 
public class MultiDimensionalCuboidsRotationStacked : MonoBehaviour
{
    public GameObject cuboidPrefab;
    float yOffset = 0.225f;
    public int arraySize;
    public float offset = 1.5f;
    public float rotationSpeed;
    private GameObject[,,] cuboidArray;
    public Gradient colorGradient;
 
    // Start is called before the first frame update
    void Start()
    {
        cuboidArray = new GameObject[arraySize, arraySize, arraySize];
        for (int i = 0; i < arraySize; i++)
        {
            for (int j = 0; j < arraySize; j++)
            {
                for (int k = 0; k < arraySize; k++)
                {
                    Vector3 cuboidPlacement = new Vector3(i * offset, k * yOffset, j * offset);
                    cuboidArray[i,j,k] = Instantiate(cuboidPrefab, cuboidPlacement, Quaternion.identity);
                    cuboidArray[i,j,k].GetComponent<Renderer>().material.color = colorGradient.Evaluate((float)k / arraySize);
                }
                
            }
        }
    }
 
    // Update is called once per frame
    void Update()
    {
        for (int i = 0; i < arraySize; i++)
        {
            for (int j = 0; j < arraySize; j++)
            {
                for (int k = 0; k < arraySize; k++)
                {
                    cuboidArray[i,j,k].transform.Rotate(Vector3.up, rotationSpeed);
                }
                
            }
        }
    }
}
{{</highlight>}}

{{< figure src="/img/MultiDimensionRotationStacked.gif" title="Three dimensional Array" width="75%">}}



### Projects
#### Project 1
Again go and play with this. Here is some inspiration.
{{< figure src="/img/MultidimensionalNoisePosition.gif" width="50%">}}
{{<expand>}}
Add Gist
{{</expand>}}
{{< figure src="/img/MultidimensionalDistancebasedSin.gif" width="50%">}}
{{<expand>}}
Add Gist
{{</expand>}}

