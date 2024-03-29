
### Getting started with Unity
So you managed your way through the Introduction and are still here. Awesome!
The first step on your Journey to learn is to actually go and download Unity. While you could just head to unity3d.com and grab the latest and greatest Version of Unity Personal, I would suggest getting the Unity Hub. Unity Hub will help you manage your Projects as well as the Versions of Unity you have installed on your machine. As you dive deeper and deeper into Unity the day will come, where you hear of a new feature and you really want to try it. 
And Unity Hub is great helper to automatically manage Versions of Unity! But both ways are obviously fine!

As you are willing to learn to code and coding is in essence a problem solving skill, I will leave the rest of the process to you.
If you struggle, from now on and for the rest of this journey the Search-Engine of your choice is your best friend!


I will show you the process of using UnityHub to manage your Projects and Unity installations.
When you Start Unity Hub it will automatically show you all your latest Projects. If you don’t have one just press the “New” Button to create One. In the next Panel you can Set the Project Name and the Location where the Project will be stored. UnityHub will create a Folder with your chosen Projectname. So no need to create that folder yourself.
You will also have to choose a Template. “3D” is the default option, yet we will use the “Lightweight RP” Settings. It will help to help our tiny projects run smoothly on mobile devices and it will also get us access to the ShaderGraph. Hit create and Unity will take a while to initialize your new project and start up the Editor.

Once Unity opens up you should see something like this:
![The Unity Editor](/img/UnityEditor.jpg)

Unitys default Layout is divided in roughly 4 parts.
The Hierarchy Window is a representation of all the Objects that are currently present in your scene. It can  also hold more than one Scene at a time. Using the arrows you explore elements further down in the hierarchy.

The “Project” Window holds all Objects that are currently inside your project. You can and should organize this using folders. Make sure to name all your files and folder because things can get messy real quick and not taking care of your Folder-Structure can end being a major source of frustration further down the line. Using rightClick you can copy, paste duplicate and even create new Objects. Info about the selected object will show up in the Inspector. (See below)
![The Unity Editor](/img/UnityProject.jpg)


The “Inspector” window shows you information on the selected object. This information mainly consists of Components. While every Object will have an “Transform” Component the rest of the List will probably differ. We will look at a lot of components over time. Just remember where to find them.
![The Unity Editor](/img/UnityInspector.jpg)

In the “Scene” View you can see all the objects in your scene. This will also include some Gizmos for Lights, Effects an Lightprobes. To move around in the scene view you need to remember three shortcuts: 
Alt + LeftClick Drag to rotate
Alt + RightClick Drag to zoom
Alt + MiddleClick Drag to pan the camera
![The Unity Editor](/img/UnityScene.jpg)

Once you select and Object using LeftClick an Gizmo will appear. The default should be the “move” Gizmo. Hover over one of the Axis and LeftClick Drag to move the Object along the selected axis. There are also tools for Rotation and Scale. To switch between the three you could use the buttons on the upper left toolbar. But please, please never do so. Use the Shortcuts:
W - Move
E - Rotate
R - Scale
If you wonder how these Shortcuts come to be. Why not “R” for Rotate, eh? Because it’s convenient for heavy user, like you will become. As your thumb will always rest on “alt” for navigation purposes, you will have quick access to the main tools for the editor.
Also this corresponds to the Industry-Standard Keyboard Shortcuts many users know from Digital Content Creation Packaged like Maya or Houdini.

There is also an alternative way to move around the viewport. If you hold down the right mouse button four squares will appear. Now you can look around by dragging the mouse and move around using the WASD keys. Try it!

Okay. That’s what you need to now for now. Let’s move forward











TODO
Principles of Coding, Principles of Design
Josef Albers at the bauhaus
He did ColorStudies which look very distinct.
We will recreate one using Unity


### Introducing the Bauhaus
Introducing the Bauhaus
While teaching programming is rather straight forward, teaching art and design is not. In the  programming sessions of  this book I can teach you the syntax of the language and it will always apply. And if you do not abide by it’s rules things won’t work. (This would not be true if we were using Javascript btw.)
Design and Art is different. Some would argue, that there are no rules. Pablo Picasso famously said, you need to learn the rules to break them. And then there was the Bauhaus, who actually aimed for that universal language of design as going so far as trying to fix the realtionship between color and and form. Wassily Kandinsky assigned yellow, red and blue to the forms triangle, rectangle and circle. While this seems outdated, a lot can be learned form their approach to teaching and understanding design.
Throughout the first chapters we will use some of their work as reference and their ideas for rules in designing things. We will complement this by their idea of experimentation. While experimenting on our designs we will also have a good chance to get our fingers accustomed to coding. 




### “Homage to the Square” in Unity
With Josef Albers “Homage to the Square” paintings as a goal, let’s head back to Unity. First we should start out be tidying our workspace. Unity projects come with some thing premade and we eanto to get rid of it! So delete everything in the Projects Folder except for the Materials, Scenes, Scripts and the packages folder.
Now create a new Scene. You can either press ‘CTRL + N’ to create a new scene or in the Project Window: RightClick -> Create -> Scene.
No let’s create our for square. In the hierarchy RightClick -> 3D Object -> Quad. Quads by default are Squares of 1x1 Unit. 
{{< expand >}}
## Planes
You could also use a plane. For now they are interchangeable. The core 
differerence is, that Quads consists of 4 Vertecies and 2 Triangles and are therefor more efficient than planes which consist many more points and triangles. For our case both are absolutley fine.
{{< /expand >}}
Now check out the Inspector with your Quad selected in the ProjectView. The Quad comes with 4 Componenents attached to it. The first component is the ‘Transform’ component. It’s jobs is to hold information about position, rotation and scale of every object in the scene. Try playing with those values to see what happens in the viewport. You can hover your mouse over the X,Y and Z Components to get a access to a slider function. Of course you can also change those value through the interaction in the viewport we discussed in the last chapter.
Next up are the Mesh Filter and Mesh Renderer. The Mesh Filter will pass the Object to the Renderer and really is nothing wen need to concern ourselves with. The Mesh Renderer contains information about how and IF the Objects is rendered in the scene. Take look at the little checkbox at it’s top. If you uncheck it, rendering of the object will be disabled.
The fourth component tat is added by default is a ‘Mesh Collider’. Mesh Colliders are Unitys way of telling the object to interact with the built in Physics System. We don’t need this so we can just delete it. To get rid of a component press the little cogwheel on the upper right corner and choose remove component.
The least thing Unity be default provides us with, is a shader. Shaders define how objects should look in our scene by considering their interaction with lights and so on.
As we are focused on trying to create a 2D Design we actually do not need any interaction with light for now, so let’s change the shader. To change it, we need a material to chnage it to! So go into your materials Folder and do `RightClick ---> Create ---> Material`. With the new Material selected, check th Inspector. Under the Dropdown choose `Unlit ---> Color`. Unlit Shaders do not react to light and directly represent the color of our choosing. By Clicking the Color you can pick the Color of your choosing in the Color Picker. Ignore everything else.
Check your Game view to inspect what you see. (Not the Scene View!) You should have a plane, but it’s lying on the floor. Use the Viewport tools to rotate have it face towards the camera.
As you now, we will need two or three more squares to fullfill our Homage to the “Homage to the Square”. Select the Objects in the Hierarchy and press `CTRL +D`. Alternatively `Rightclick ---> Duplicate` will do the trick as well.
To actually change the Colors of each new Quad, we need two new Materials as well. So duplicate them and assign them a new color and assign the materials to the Quads, so that each Quad has it’s own material and Color.
If you go into gameview, you will still only see one plane. This is because right now all of our planes are in the exact same position in space. Also they have the exact same size. So not try to push some of them slightly to the back and scale them up and position them to finish your own personal “Hommage to the Quad”.


