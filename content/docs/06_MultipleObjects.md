### Multiple Object Workflow
If you followed along with some of the examples, you probably realized we are doing a lot of manual labor in changing things on the Unity Editor itself. Each Square has to get the new Script and so forth. Then again programming is a lazy mans art. The less manual labor we have to do the better.
In this Chapter we will introduce ways to handle multiple Squares at once. And Squares - of course cpuld be anything in the end. To do this conveniently in Unity we need to look at three Concepts:
1. Prefabs and Instantiation
2. Lists and Arrays
3. Loops
In short, we will create objects through Instantiation. We will the use Lists to hold track of them and loops to iterate over these lists.
What’s even better is, it opens up a lot of creative possibilities and ideas to talk about! 

### Prefabs and Instantiation
Instantiation is the process of creating Objects from a script and it is tightly intertwined with the Concept of Prefabs. Prefabs are “prefabricated” Objects we can “save” in the project window.
Creating Prefabs is superbly simple. You create the Object you want to create in the Hierarchy and then drag and drop it into the Project View.
TODO GIF PREFAB
The tiny cube in front of the object turns blue if Unity knows about this object as an Prefab. It’s often advisable to create a specific folder for all your prefabs. The great thing is that Unity will keep all of it’s components attached to the prefab.
##### You may want to dublicate your scene before following along.
So if you go ahead and take a square with a script for movement already attached to it you will be able to instantiate it.
Once you have created a prefab from an GameObject you can go ahead and delete it from the hierarchy.
### Instantiation
Next we will need to create a script to actually handle the creation of all our stuff and because scripts in Unity can’t exists in empty space, we need to create a GameObject for this as well. Technically any object would work, yet an “Empty Object” would of course be the ideal choice. Empties only consist of a transform component and thus have no visual representation in the scene. Rename your Empty to something like “ScriptHolder” or “Manager”. 
First we have to find a way to grab hold of our prefabed square. In Unity all Objects (that inherit from Monobehaviour) can be referenced as GameObject. So let’s create a variable for our square.
{{<highlight c>}}
public GameObject squarePrefab;
{{</highlight>}}
Now go back to Unity and check the Inspector. You will see a field named squarePrefab. You can now drag and drop the prefab you created from the Project view into the field on the inspector.
Now the script *knows* about the prefab. Next we need to actually create an actual instance at runtime:
{{<highlight c>}}
Instantiate(squarePrefab, Vector3.back, Quaternion.identity);
{{</highlight>}}
The instantiate Method takes 3 argumentts: 1. The Object we want to Instantiate, A  Vector as Position in Space, and a Rotation. Rotation is passed as Quaternion. For now,  just use Quaternion.identity; Quaternions are scary things. We will deal with them later.
If you run your scene now, you should have one one Square moving around. 
Go ahead and duplicate that line.
It should give you two Squares and yet you will probably only see one.
Both are created in exactly the same space and Size again. Also both have the same color.
So we need to find a way to access a gameObject after instantiation. To do that we can just assign the created Object to variable the moment we create it:
{{<highlight c>}}
	var Square =Instantiate(_SquarePrefab, Vector3.back, Quaternion.identity);
{{</highlight>}}
{{<expand>}}
### the ‘var’ Keyword
You might stumbled across the ‘var’ Keyword here. You will see code that never uses ‘var’ and code which makes a lot use of it. Generally speaking you should only use it when through the context it is unmistakeable which Type is referenced. This is mostly true for “Object stuff”. To keep it simple for now. As an Example:
`GameObject myGameOject = new GameObject();`
This would create a new empty GameObject. But the line of code isn’t a beauty, is it? That’s where var comes in:
`var myGameObject = new GameObject();`
Don’t worry about it too much for now. This will become second nature over time.
{{</expand>}}
Now we have a variable for our square. With this variable we can change the square from this script just like the way we used to with the script which was directly attached to the square itself. All we have to chang is adding Square in front of it.
{{<highlight c>}}
Square.transform.position = new Vector3(0,0,0);
{{</highlight>}}
To actually start recreating our sketch, we need two other squares with another variable.
{{< highlight c>}}
var Square =Instantiate(_SquarePrefab, Vector3.back, Quaternion.identity);
var SquareM =Instantiate(_SquarePrefab, Vector3.back, Quaternion.identity);
var SquareS =Instantiate(_SquarePrefab, Vector3.back, Quaternion.identity);
{{</highlight>}}
If you run this, we still face the problem of all squares overlapping in the exact same space. 


Now this still is waaaaay too much manual labour for being in any kind practical. What if we needed a hundered or a thousand squares? You’d quit coding immediatly. Well don’t!

### For Loops
To be able to handle many Objects (or any kind repeating process) programmers came up with loops. Loops are blocks of code thate are executed over and over again until a certain condition is met. Maybe the most common implementation of a loop is the “for loop”. 
For Loops in C# need three things to work: Initializer, condition and iterator. Think of it as having a jar of cookies and you are allowed to eat 50 cookies in a week. So you need to make sure how many you have eaten. So you take a piece of paper and start a tally sheet. This tally sheet is your initializer. The Initializer is just creating a variableto keep track of a number. Then each time you want a cookie you check wether you are still allowed to eat a cookie. That’s the condition. Once you have eaten the cookie you add one. That’s done using the iterator.
Actually eating the cookie is the code the run. That’s wrapped in curly braces again.
{{<highlight c>}}
for (int i = 0; i < 5; i++)
{
    Debug.Log(i);
}
{{</highlight>}}

A For Loops starts with the `for` Keyword followed by brackets. The first thing is our tally list / Initializer. It works exaclty like creating any other variable in Unity. The three parts of a loop separeted by a semicolon. Next up is the condition. Conditions in for loops check if you counter is higher or lower then a certain threshold and if it evaluates to false the loop will stop. Last is the iterator which counts up. In this case the `i++` just means the variable I will be increased by one after each iteration. You could also put `i+2` to always add two to the number.
In the curly brackets follows the code to run. Here we just run a counter in the console.

So that’s it for the theory. Let’s take a look at this in action.
As we want to stay flexible with this, we will create some variables to first.
{{<highlight c>}}
public GameObject SquarePrefab; public int numberOfSquares = 3; public float shrink = 0.1f; private List<GameObject> squareList = new List<GameObject>(); public Gradient myColors = new Gradient();
{{</highlight>}}

Of course we still have the reference to our prefab in place. Next we create a variable to propagte the number of squares we want to create to the Unity Editor. We will also need to somehow define a way of scaling our squares with each iteration, so we add a shrinking factor.
Next up is a `List<GameObject>` object. As it’s an Object we ne to create it using the `new` keyword. Lists are pretty much exactly what you expect them to be. They hold a List of things, but we need to specify what kind of things we want it to keep track of. In our case that’s GameObjects.
Last up is a Gradient. We can define a Gradient and the evaluate the Color at a certain point. This will help us define good and harmonious colors. Defining the colors willl be done in the Unity Editor with the color picker.

So now we need to look at the for loop which goes into the `Start()`  Function.
{{<highlight c>}}
for (int i = 0; i < numberOfSquares; i++) 	{
	}
{{</highlight>}}

Starting the expressionwith the `for` Keyword we create a counter variable `i` and set it to 0. You could start with a different number, but typically 0 makes the most sense.
Next up is the Condition to check for after each iteration. Here we use the variable we created earlier. This allows for artist control inside the Unity Editor. The last bit is the iterator. So this initializes our loop. Let’s look at the Code within the loop line by line.

{{<highlight c>}}
for (int i = 0; i < numberOfSquares; i++) 	{     squareList.Add(Instantiate(SquarePrefab, Vector3.back * i/100, Quaternion.identity)); 
{{</highlight>}}

I guess this is the first line that could look really intimidating, but it’s not. Just try to read it kinda like english.
To the `squareList` we `Add` something. That something does not exist yet, so we Instantiate it, just like we did before. What do we Instatntiate? Our `SquarePrefab`. Where? At a Vector pointing back multiplied by out Initializer divided by 100.
This is what makes loops powerful. On the first iteration `i` equals 0 so, the position of the first square will be `(0,0,0)`.
In the next iteration `i` equals 1 and `i/100` will equate to 0.01. So it will be slightly offset. Changing the value of division would change this factor. And of course we could have another variable here.
So not so scary after all, right?
So let’s check the next line.
{{<highlight c>}}
squareList[i].transform.localScale *= 1 - (shrink * i);
{{</highlight>}}
Here we access an item in a list. Item `i`.
We just added that item one line prior and counting lists start at 0. So we access exactly the item we just created.
We then grab the transform component and change the localScale by multiplying it by some value.  Here we multiply the shrinking by `i` again. So the later the comes in the list, the smaller it will be.

So next up:
{{<highlight c>}}
squareList[i].GetComponent<MovingAlbers>().multiplier = 1 - ((i+1) * shrink * 2);
{{</highlight>}}
Here we again access an item in the List based on `i`. Now we access our MovingAlbers script and change the multiplier (which was a scaling factor on movement range). Here again we use `i` and our shrink value to modify the values.
{{<highlight c>}}
squareList[i].GetComponent<Renderer>().material.color = myColors.Evaluate((float)(i+1)/(float)numberOfSquares);
{{</highlight>}}
Finally we set the Color of the squares by evaluating a Gradient. Gradient Evaluation is done by defining a number between 0 and 1. So we divide the current value of `i` by the number of squares we are going to create. Because both of the values are integers, we need to convert them using `(float)`. Otherwise we would get an integer back and that would not be helpful of course.
Once you have set this up, make sure to define a Gradient in the UnityEditor. Otherwise it will have just one color and you will go bug hunting for nothing... (I’ve been there...)











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
