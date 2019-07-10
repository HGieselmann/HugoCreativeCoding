
### Multiple Object Workflow
If you followed along with some of the examples, you probably realized we are doing a lot of manual labor in changing things on the Unity Editor itself. Each Square has to get the new Script and so forth. Then again programming is a lazy mans art. The less manual labor we have to the better.
In this Chapter we will introduce ways to handle multiple Squares at once. And Squares of course in the end could be anything. To do this convenienty in Unity we need  to look at three Concepts:
1. Prefabs and Instantiation
2. Lists and Arrays
3. Loops
In short, we will create objects through Instantiation. We will the use Lists to hold track of them and loops to iterate over these lists.
What’s even better is, it opens up a lot of creative possibilities and ideas to talk about! 

### Prefabs
Instantiation is the process of creating Objects from a script and it is tightly intertwined with the Concept of Prefabs. Prefabs are “prefabricated” Objects we can “save” in the project window.
Creating Prefabs is superbly simple. You create the Object you want to create in the Hierarchy and then drag and drop it into the Project View.
TODO GIF PREFAB
The tiny cube in front of the object turn blue if Unity knows about this object as an Prefab. It’s often advisable to create a specific folder for all your prefabs. The great thing is that Unity will keep all of it’s components attached to the prefab.
##### You may want to dublicate your scene before following along.
So if you go ahead and take a square with a script for movement already attached to it you will be able touse it through instantiation.
Once you have created a prefab from an GameObject you can go ahead and save it from the hierarchy.
### Instantiation
Next we will need to create a script to actually handle the creation of all our stuff and because scripts in Unity can’t exists in empty space, we need to create a GameObject for this as well. Technically any object would work, yet an “Empty Object” would of course be the ideal choice. Empties only consist of a transform component and thus have no visual representation in the scene. Rename your Empty to something like “ScriptHolder” or “Manager”. 
Fiorst we have to find a way to grab hold of our prefabed square. In Unity all Objects (that inherit from Monobehaviour) can be referenced as GameObject. So let’s create a variable for our square.
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





