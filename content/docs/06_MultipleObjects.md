### Multiple Object Workflow
If you followed along with some of the examples, you probably realized we are doing a lot of manual labor in changing things on the Unity Editor itself. Each Cuboid has to get the new Script and so forth. Then again programming is a lazy mans art. The less manual labor we have to do the better.
With the concepts introduced in this chapter, we will be able handle lots and lots of objects simultaneously. Hence it will also allow us to create more complex sketches.
We will also look at interaction between multiple scripts. Finally keywords like `private` and `public` will hopefully make more sense.
Thus in this Chapter we will introduce ways to create and handle multiple cuboids at runtime. And cuboids - of course could be anything really. To do this conveniently in Unity we need to look at three Concepts:
1. Prefabs and Instantiation
2. Arrays or Lists
3. Loops
In short, we will create objects through Instantiation. We will the use Arrays and Lists to keep track of them and loops to iterate over them
What’s even better is, it opens up a lot of creative possibilities and ideas to talk about! 

### Prefabs and Instantiation
Instantiation is the process of creating Objects from a script and it is tightly intertwined with the Concept of Prefabs. Prefabs are “prefabricated” Objects we can “save” form the project view. They are in most cases the objects we want to then create through code.
Creating Prefabs is superbly simple. Any object you have in your scene can be turned into a prefab. All you have to do is drag an item from the hierarchy into the project view. 
TODO GIF PREFAB
The tiny cube in front of the object turns blue if Unity knows about this object as an Prefab. It’s often advisable to create a specific folder for all your prefabs. The great thing is that Unity will keep all of it’s components attached to the prefab. But it also opens up room for some consideration later on. Any behaviour we have added to a prefab will be there once we create an instance of it. This can be what you want, but it’s not necessarily so.
Once you have created a prefab from an GameObject you can go ahead and delete it from the hierarchy.


### Instantiation
With an prefab ready, we will need to create a script to actually handle the creation/instantiation of all our cuboids and because scripts in Unity can’t exists in empty space, we need to create a GameObject to hold our script. Technically any object would work, yet an “Empty Object” would of course be the ideal choice. Empties only consist of a transform component and thus have no visual representation in the scene, thus you are less likely to accidentally delete them. Rename your Empty to something like “ScriptHolder” or “Manager”. 
First we have to find a way to grab hold of our prefabricated cuboid. In Unity all Objects (that inherit from Monobehaviour - we’ll discuss this in Chapter 08) can be referenced as GameObject. So let’s create a variable of type `GameObject` for our cuboid.
{{<highlight c>}}
public GameObject cuboidPrefab;
{{</highlight>}}
Now go back to Unity and check the Inspector. You will see a field named cuboidPrefab. You can now drag and drop the prefab you created from the Project view into the field on the inspector.
Add Gif here
Now the script *knows* about the prefab. You might argue, that this process feels a little strange, and I am with you. I tend to forget this step and run into an error. But you’ll get used to it!
Next we need to actually create an actual instance at runtime:
{{<highlight c>}}
Instantiate(cuboidPrefab, Vector3.zero, Quaternion.identity);
{{</highlight>}}
The instantiate Method takes three argumentts: 
1. The Object we want to Instantiate 
2. A Vector as Position in Space 
3. Rotation passed as a Quaternion. 
For now,  just use `Quaternion.identity;`. Quaternions are scary things and `Quaternion.identity` will place them in the exact state you created the Prefab in, so that’s very, very likely correct anyway.
If you run your scene now, you should have one Cuboid moving around, based on the script you had attached to it, when creating the prefab.
Go ahead and duplicate that line. It should give you two cuboids and yet you will probably only see one. Both are created in exactly the same space and size. But you should be able to see two of them in the hierarchy.
So we need to find a way to access a gameObject after instantiation. To do that we can just assign the created Object to variable the moment we create it:
{{<highlight c>}}
	var cuboid = Instantiate(cuboidPrefab, Vector3.back, Quaternion.identity);
{{</highlight>}}
{{<expand>}}
#### the ‘var’ Keyword
You might stumbled across the ‘var’ Keyword here. You will see code that never uses ‘var’ and code which makes a lot use of it. Generally speaking you should only use it when through the context it is unmistakeable which Type is referenced. This is mostly true for “Object stuff”. To keep it simple for now. As an Example:
`GameObject myGameOject = new GameObject();`
This would create a new empty GameObject. But the line of code isn’t a beauty, is it? That’s where var comes in:
`var myGameObject = new GameObject();`
Don’t worry about it too much for now. This will become second nature over time.
{{</expand>}}
Now we have a variable for our cuboid. This variable allows us to access the the cuboid and all the properties of it, that are actually public. This is the first time `private` and `public` actually become relevant for us in a scripting sense.
{{<highlight c>}}
cuboid.transform.position = new Vector3(0,0,0);
{{</highlight>}}
So to actually recreate our Homage to the cuboid we would need to do this over and over again and then adjusting things and... nah...  We are not going to do that. As I said before. One core idea in programming is DRY - Don’t repeat yourself. Thus we are not going to do that!

### For Loops
To be able to handle many Objects (or any kind repeating process) people came up with loops. Loops are blocks of code that are executed over and over again until a certain condition is met. Maybe the most common implementation of a loop is the “for loop”. 
For Loops in C# need three things to work: Initializer, condition and iterator. Think of it as having a jar of cookies and you are allowed to eat 50 cookies in a week. So you need to make sure how many you have eaten so far. So you take a piece of paper and start a tally sheet. This tally sheet is your initializer. The Initializer is just creating a variable to keep track of a number. Then each time you want a cookie you check whether you are still allowed to eat a cookie or if you already had 50. That’s the condition. Once you have eaten the cookie you add one to your tally sheet. That’s done using the iterator.
Actually eating the cookie is the code run in the loop. That’s wrapped in curly braces again.
{{<highlight c>}}
for (int i = 0; i < 5; i++)
{
    Debug.Log(i);
}
{{</highlight>}}

A *for loop* starts with the `for` Keyword followed by parentheses. The first thing is our tally list / Initializer. It works exactly like creating any other variable in Unity, but you *have* to initialize it. What’s also to note is: Counting in computer science almost always starts with 0. Thus we will start with `int i = 0`! The three parts of a loop are separated by a semicolon. Next up is the condition. Conditions in for loops check if your counter is higher or lower then a certain threshold and if it evaluates to false the loop will stop. Last is the iterator which counts up. In this case the `i++` just means the variable `i` will be increased by one after each iteration. You could also put `i+1`.Actually you could advance your initializer in any stepsize: `i + 2`, `i+100`. They all work fine.
In the curly brackets follows the code to run. In the above counter we just print the value of our counter `i` to the console.

### Arrays
That’s it for the theory, let put this into practice. Earlier, when were discussing Instantiation, we said we need a variable to create a reference to our objects. But creating five variables, each to hold a cuboid would be very inefficient again. That’s why we also need to introduce Arrays. Arrays hold many things of one same type. A list in essence, except that they aren’t really list because list exist as well and you see.. this is messed up.
Anyway... Arrays hold things of the same *type*. Like *float* or *integer*. Or *GameObject*! Creating Arrays is simple. You create them like any variable, but add `[]` after the type.
{{<highlight c>}}
private GameObject[] myGameObjectArray;
{{</highlight>}}
Now we have created the Array, but we didn’t initialize it and thus can’t use it. The thing with Arrays is, that they always have a fixed length. So in the moment you *initialize* the array, you need to specify how many items you want to store in your list. For our cuboids, it’s as simple as this:
{{<highlight c>}}
private GameObject[] cuboids = new GameObject[5];
{{</highlight>}}
With arrays we simply have to specify the length of the Array again in brackets. But what if you wanted to do this based on a variable? You can create the variable for this on global scope and then initialize the array in `Start()` or `Update()`.
{{<highlight c>}}
    private GameObject[] myGameObjects;
    public int arraySize = 5;
    // Start is called before the first frame update
    void Start()
    {
        myGameObjects = new GameObject[arraySize];
    }
{{</highlight>}}
So you have some flexibility, but can’t change the actual length of the array. To finally access things inside an array we use the bracket notation again.
{{<highlight c>}}
	Debug.Log(myGameObjects[0]);
{{</highlight>}}
This would print the first object in the Array to the console. As we said earlier, counting always starts with `0`! So now let’s look at actually making use of this:
{{<highlight c>}}
    public GameObject myPrefab;
    private GameObject[] myGameObjects;
    public int arraySize = 5;
    // Start is called before the first frame update
    void Start()
    {
        myGameObjects = new GameObject[arraySize];
        for(int i = 0; i < arraySize; i++)
        {
            myGameObjects[i] = Instantiate(myPrefab, Vector3.up * i, Quaternion.identity);
        }
    }
{{</highlight>}}
This code incorporates everything we have covered so far. We first create a variable for a prefab. We then create a variable for an array of Gameobjects and also create a variable for the size of the array. In `Start()` we then initialize the array to the size of the variable. Henceforth it can hold five objects right now. But at the moment all slots are empty.
Next we create a *for loop* and it’s condition is that our initializer is smaller than our `arraySize` variable. During the loop we access each slot of the list by it’s number, using the iterator. We also use the iterator as an multiplier for the position, thus shifting each object up by one.
Add result here
This might seem complicated at first, but it’s not too bad, once you have created a few arrays and written a few for loops. It’s also very, very powerful! As you can image we could easily set the value for our `arraySize` to `10`, `100` or even a thousand. Think about how long it would take to create a hundred of these cuboids by hand!
Before we take this concept even further, I suggest you try to recreate some of the examples we did in earlier chapters using arrays and for loops. Maybe you can also come up with new variations.
Add in three examples with Scripts applied to prefabs

All of these use the idea of having the behavior attached to the prefab itself. This can, or can not be the most practical way to go. We could also handle all of this directly through one script. Or we could add the behavior at runtime to the cuboid prefabs. In our case of some moving cuboids, all approaches could be equally fine and the way you implement this really comes down to taste. In more complex situations there might be a stronger indication to where a script is placed in a useful fashion.
I want to show you the other possibilities not only for the sake of completeness but also because it allows us to discuss script interaction. Thus far all of our scripts were self contained little programs. They had no way of interacting or properly with one another. The great thing in this is, you could already know how to do this, you might just not be aware of that. 
{{<highlight c>}}
using UnityEngine;

public class Tests : MonoBehaviour
{
    public GameObject myPrefab;
    private GameObject[] myGameObjects;
    public int arraySize = 5;
    // Start is called before the first frame update
    void Start()
    {
        myGameObjects = new GameObject[arraySize];
        myGameObjects[0].transform.position = Vector3.zero;

        for(int i = 0; i < arraySize; i++)
        {
            myGameObjects[i] = Instantiate(myPrefab, Vector3.up * i, Quaternion.identity);
            myGameObjects[i].AddComponent<Cuboid_MovingUp>();
        }
    }
}
{{</highlight>}}
This is based on the script we discussed earlier. Yet this one assumes you don’t have a script attached to your prefab. Thus what we do is attach our behavior at runtime. Using `AddComponent<>()` we can add any script or component Unity offers. Any script you have created in your project can simply be added here. So this script could handle all of your variants. All you needed to do was to change the component you add.


Lists



### For-each Loops
“For each loops” work very similar, except you don’t need have to bother with the iterator and the initializer, because a for each loop executes over each item in a list or array.
Their syntax is very straight forward as well.
We will extend our script from the For Loop with and For Each loop, that runs in the Update function. We will reuse our idea of Color shifting and apply it to all of the squares by iterating over them.
{{<highlight c>}}
foreach (GameObject currentGameObject in squareList) {     float h,s,v;     Color currentColor = currentGameObject.GetComponent<Renderer>().material.color;     Color.RGBToHSV(currentColor, out h, out s, out v);     h += 0.001f;     if(h > 1){         h = 0;     }     currentGameObject.GetComponent<Renderer>().material.color = Color.HSVToRGB(h,s,v); }

{{</highlight>}}

As you can see the Syntax here is relativley straight forward: You start with the `foreach` Keyword and follow that up by the Type of Object you want to iterate over. We have a list of GameObjects, so we iterate over those. Then we create a name, which allows us to actually access the GameObject in each iteration. This is what `squareList[i]` would be in for loops. Lastly we just specify the list we want to iterate over after puttig the `in` Keyword.
All of this actually reads almost like english, which is nice. On the downside, we are not automatically handed an iterator.
Both Loops are useful in their own right, so choose the appropriate or just stay with the for loop, that’s fine too.

### While Loops
There is yet another type of loop. The while loop.
While loops are the most basic type of loop and essentially just run as long as a condition stays true. Think of the Update function. It loops each frame, but of course has now counter to finish after a certain amount of Frames. That would be silly. Essentially it will loop as long as the game is running.
{{<highlight c>}}
while(true){
	//Code to run
}
{{</highlight>}}
That would be an infinite loop. `true` can never just become false. So this will run forever.
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
This code would actually work just fine. It’s essentially recreating the for loop, we have been looking at earlier, we just created in manually.
But you could of course use this in cases, when you want to base the iteration on some kind of outside variable. Just make sure to be able to change the value from inside the while loop.

There 


### Do-While Loops
There is one last kind of loop which C# offers. The “do-while” loop. As the name suggests it’s very tightly entangled with the while loop. It’s special feature is, that it will always execute at least once, because the evaluation of the condition follows after the first iteration step.
{{<highlight c>}}
int i = 0;
do 
{
    Debug.Log(i);
    i++;
} while (i < 5);
{{</highlight>}}
As you can imagine, this one doen’t bring that much to the table, so we are not working out an example for this one. But I want you to be aware of it’s existence and it certainly has it’s use-cases.


