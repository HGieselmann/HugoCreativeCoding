
### Introducing the Bauhaus
Introducing the Bauhaus
While teaching programming is rather straight forward, teaching art and design is not. In the  programming sessions of  this book I can teach you the syntax of the language and it will always apply. And if you do not abide by it’s rules things won’t work.
Design and Art is different. Some would argue, that there are no rules. Pablo Picasso famously said, you need to learn the rules to break them. And then there was the Bauhaus, who actually aimed for that universal language of design as going so far as trying to fix the realtionship between color and and form. Wassily Kandinsky assigned yellow, red and blue to the forms triangle, rectangle and circle. While this seems outdated, a lot can be learned form their approach to teaching and understanding design.


### Installing Unity

The first step on your Journey to learn is to actually go ahead to download and install Unity. While you could just head to unity3d.com and grab the latest and greatest version of Unity, I would suggest getting the Unity Hub. The Unity Hub will help you manage your Projects as well as the Versions of Unity you have installed on your machine. As you dive deeper and deeper into Unity the day will come, where you hear of a new feature and you really want to explore it. Then you can easily install any additional version directly from Unity Hub and manage all the versions of Unity you have currently installed. But just grabbing the current version is obviously just fine as well.

I will assume, you will manage to download install Unity Hub yourself. So let’s look at the process of managing Unity Versions and more importantly Projects with Unity Hub.
TODO Add Unity Hub Version Management as soon, as 2019.4 is out!
When you Start Unity Hub it will automatically show you all your latest Projects. If you don’t have one, just press the “New” Button to create One. In the next Panel you can Set the Project Name and the Location where the Project will be stored. UnityHub will create a Folder with your chosen Projectname. So no need to create that folder yourself.
You will also have to choose a Template. “3D” is the default option. You will also have options for 2D and depending on the version you installed for “Lightweight RP / LWRP” or “High Definition Renderpipeline / HDRP”. It could also be, that Lightweight Renderpipeline is alread called “Universal Renderpipeline”. Sooner rather than later this will become the default. Yet we will for now go with the classic “3D” version. Hit create and Unity will take a while to initialize your new project and start up the Editor.

Once Unity opens up you should see something like this:
![The Unity Editor](/img/UnityEditor.jpg)

Unitys default Layout is divided in roughly 4 parts.
The Hierarchy Window is a representation of all the Objects that are currently present in your scene. It can  also hold more than one Scene at a time. Using the black arrows you can collapse or expand the hierarchy depending on your needs.
![The Unity Editor](/img/UnityHierarchyEditor.jpg)

The “Project” Window holds all Objects that are currently inside your project. You can browse this just like any directories in your operating system. You can also create folders organize yourself. If you were to browse to your project Folder on your hard drive you would actually see exactly this structure inside the “Assets” folder. Make sure to name all your files and folders properly from the get go, because things can get messy real quick and not taking care of your Folder-Structure can end being a major source of frustration further down the line. Using rightClick you can copy, paste, duplicate and even create new Objects. Info about the selected object will show up in the Inspector. (See below)
![The Unity Editor](/img/UnityProject.jpg)


The “Inspector” window shows you information on the selected object. This information mainly consists of so calles “Components”. While every Object will have an “Transform” Component the rest of the List will probably differ. We will look at a lot of components over time. Just remember where to find them.
![The Unity Editor](/img/UnityInspector.jpg)

The “Scene” view is your portal to viewing you current Scene. Here you move around freely and manipulate the objects in your scene using “Gizmos”. To move around in the scene view you need to remember three shortcuts: 
Alt + LeftClick Drag to rotate
Alt + RightClick Drag to zoom
Alt + MiddleClick Drag to pan the camera
![The Unity Editor](/img/UnityScene.jpg)

Once you select and Object using LeftClick an Gizmo will appear. The default should be the “move” Gizmo. Hover over one of the Axis and LeftClick Drag to move the Object along the selected axis. There are also tools for Rotation and Scale. To switch between the three you could use the buttons on the upper left toolbar. But please, please never do so. Use the Shortcuts:
W - Move
E - Rotate
R - Scale
{{<expand>}}
If you wonder how these Shortcuts come to be. Why not “R” for Rotate? Because it’s convenient for heavy users. As your thumb will always rest on “alt” for navigation purposes, you will have quick access to the main tools for the editor.
Also this corresponds to the Industry-Standard Keyboard Shortcuts many users know from Digital Content Creation Packaged like Maya or Houdini.
{{</expand>}}

There is also an alternative way to move around the viewport. If you hold down the right mouse button four squares will appear. Now you can look around by dragging the mouse and move around using the WASD keys. You can try both navigation styles and see which one fits you best.


### “Homage to the Square” in Unity

![Josef Albers “Hommage To the Square” on a german stamp](/img/stampAlbers.jpg)

With Josef Albers “Homage to the Square” paintings as a goal, let’s head back to Unity. First we should start out be tidying our workspace. Unity projects come with some thing premade and we want to get rid of them! So delete everything in the Projects Folder except for the Materials, Scenes, Scripts and the packages folder.

Now create a new Scene. You can either press ‘CTRL + N’ to create a new scene or in the Project Window: RightClick -> Create -> Scene.
No let’s create our for squares. In the hierarchy RightClick -> 3D Object -> Quad. Quads by default are Squares of 1x1 Unit. 
{{< expand >}}
## Planes
You could also use a plane. For now they are interchangeable. The core differerence is, that Quads consists of 4 Vertecies and 2 Triangles and are therefore more efficient than planes which consist of many more points and triangles. For our case both are absolutely fine.
{{< /expand >}}
Now check out the Inspector with your Quad selected in the ProjectView. The Quad comes with 4 Componenents attached to it. The first component is the ‘Transform’ component. It’s jobs is to hold information about position, rotation and scale of every object in the scene. Try playing with those values to see what happens in the viewport. You can hover your mouse over the X,Y and Z Components to get a access to a slider function. Of course you can also change those value through the interaction in the viewport we discussed in the last chapter.
TODO Image of selected Inspector
Next up are the Mesh Filter and Mesh Renderer. The Mesh Filter will pass the Object to the Renderer and really is nothing wen need to concern ourselves with. The Mesh Renderer contains information about how and IF the Objects is rendered in the scene. Take look at the little checkbox at it’s top. If you uncheck it, rendering of the object will be disabled.
The fourth component tat is added by default is a ‘Mesh Collider’. Mesh Colliders are Unitys way of telling the object to interact with the built in Physics System. We don’t need this so we can just delete it. To get rid of a component press the little cogwheel on the upper right corner and choose remove component.
The least thing Unity be default provides us with, is a shader. Shaders define how objects should look in our scene by considering their interaction with lights and so on.
As we are focused on trying to create a 2D Design we actually do not need any interaction with light for now, so let’s change the shader. To change it, we need a material to chnage it to! So go into your materials Folder and do `RightClick ---> Create ---> Material`. With the new Material selected, check th Inspector. Under the Dropdown choose `Unlit ---> Color`. Unlit Shaders do not react to light and directly represent the color of our choosing. By Clicking the Color you can pick the Color of your choosing in the Color Picker. Ignore everything else.
Check your Game view to inspect what you see. (Not the Scene View!) You should have a plane, but it’s lying on the floor. Use the Viewport tools to rotate it around until it face directly towards the camera.
As you know, we will need two or three more squares to fulfill our Homage to the “Homage to the Square”. Select the Objects in the Hierarchy and press “CTRL + D”. Alternatively Rightclick ---> Duplicate will do the trick as well.
To actually change the Colors of each new Quad, we need two new Materials as well. So duplicate them and assign them a new color and assign the materials to the Quads, so that each Quad has it’s own material and Color.
If you go into gameview, you will still only see one plane. This is because right now all of our planes are in the exact same position in space. Also they have the exact same size. So try to push some of them slightly to the back and scale them up and position them to finish your own personal “Hommage to the Quad”.
![The Unity Editor](/img/staticAlbers.png)




### Project - Q 1 Suprematistic
The first simple exercise is just about getting used to navigating the interface and getting used to positioning, rotating and scaling Objects. You will also need to create Materials in the Project View and assign them to your Objects. As an inspiration for our work I’d like to look at another Bauhaus Artist: Laszlo Moholy-Nagy. 
Laszlo Moholy Nagy (1895 - 1946) was invited to the Bauhaus in 1923 by Walter Gropius. Moholy-Nagy was strongly influenced by constructivism and set a stronger industrialized tone at the school. He was braught in to teach the foundational course together with Josef Albers as well as new leader of the metal workshop. He at the Bauhaus till  1928 but later became director at the new Bauhaus in Chicago.
In 1923 Laszlo Moholy-Nagy created the painting “Q 1 Suprematisctic” (1923, Oil on canvas). 
![Q 1 Suprematistic by Laszlo Moholy-Nagy](/img/Laszlo-moholy-nagy-q-1-suprematistic.jpg)
As the title suggests it references the “Suprematism”, a russian art movement which focused on basic geometric shapes, just like the Bauhaus. As we are limited to basic primitives shapes in Unity as well - at least out of the box - this is a great way to get started playing around.

Hints on getting this done:
- Of course this is a painting and thus two-dimensional, but we will recreate this using primarily the three-dimensional primitives
- You can either flatten your shapes or use an orthogonal Projection on your camera
- For material try using Unlit > Color and Sprite > default

So this was my result in recreating his painting. You don’t have to be super precise - this is just an exercise to get you familiar with navigating the Unity editor.
![A Unity version of Q 1 Suprematistic](/img/UnitySuprematisticQ1Nagy.jpg)
If “Q 1 Suprematistic” is not your taste, look for something else online as inspiration. Or directly move on to the next project which is completly void of any Bauhaus influences.

### Environment Design
In this second challenge you have a lot more freedom to create your own. I created and asset pack full of low poly Objects. These should be enough to create small environment scenes. Maybe you can even find a way to tell a story with your image. I suggest looking for inspiration and reference online as well.
Of course you can use these Assets in any other scene you want to create. 
Explain how to download an import these assets.

{{<expand>}}
### Low Poly Models
All 3D models consists of three essential elements: Points, Lines and Planes. (Hello Mr. Kandinsky!) But mathematics came in and said: Let’s use our terms and call them: Vertex, edge and polygon. So in the context of 3D the names stuck.
Low poly objects thus are object which consist only of a few planes or polygons. This helps with performance on lower end devices but also has turned into a full on art style for illustrations and video games.
### How to create them?
If you are completely new to the world of 3D, you might as yourself how I created these. I used the free open-source software Blender. You can grab it at www.blender.org. To learn to create object like these I suggest checking out the Youtube Channel of Grant Abbit. He has some good Videos on creating low poly works.
{{</expand>}}




TODO
Build scene
Build Assets
