### Installing Unity

The first step on your Journey to learn is to actually go ahead to download and install Unity. While you could just head to unity3d.com and grab the latest and greatest version of Unity, I would suggest getting the Unity Hub. The Unity Hub will help you manage your Projects as well as the Versions of Unity you have installed on your machine. As you dive deeper and deeper into Unity the day will come, where you hear of a new feature and you really want to explore it. Then you can easily install any additional version directly from Unity Hub and manage all the versions of Unity you have currently installed. It will also remember in which version you opened a project last time. But just grabbing the current version is obviously just fine as well. If you go for the latter, choose an “LTS” version, like 2019.4. LTS is short for longtime support and has the best chances of getting all bugs fixed.

I will assume, you will manage to download install Unity Hub yourself. So let’s look at the process of managing Unity Versions and more importantly Projects with Unity Hub.
TODO Add Unity Hub Version Management as soon, as 2019.4 is out!
When you Start Unity Hub it will automatically show you all your latest Projects. If you don’t have one, just press the “New” Button to create One. In the next Panel you can Set the Project Name and the Location where the Project will be stored. UnityHub will create a Folder with your chosen Project name. So no need to create that folder yourself.
You will also have to choose a Template. “3D” is the default option. You will also have options for 2D and depending on the version you installed for “Lightweight RP / LWRP” or “High Definition Renderpipeline / HDRP”. It could also be, that Lightweight Renderpipeline is already called “Universal Renderpipeline”. Sooner rather than later this will become the default. Yet we will for now go with the classic “3D” version. Hit create and Unity will take a while to initialize your new project and start up the Editor.

Once Unity opens up you should see something like this:
![The Unity Editor](/img/UnityEditor.jpg)

Unitys default Layout is divided in roughly 4 parts.
The Hierarchy Window is a representation of all the Objects that are currently present in your scene. Using the black arrows you can collapse or expand the hierarchy depending on your needs. On the top you will see a dropdown arrow as well, because Unity can open multiple scenes at once.
![The Unity Editor](/img/UnityHierarchyEditor.jpg)

The “Project” Window holds all Objects that are currently inside your project. You can browse this just like any directories in your operating system. You can also create folders to organize yourself. If you were to browse to your project Folder on your hard drive you would actually see exactly this structure inside the “Assets” folder. Make sure to name all your files and folders properly from the get go, because things can get messy real quick and not taking care of your Folder-Structure can end being a major source of frustration further down the line. Using right-click you can copy, paste, duplicate and even create new Objects. Info about the selected object will show up in the Inspector. (See below)
![The Unity Editor](/img/UnityProject.jpg)


The “Inspector” window shows you information on the selected object. This information mainly consists of so called “Components”. While every Object will have a “Transform” Component the rest of the List will probably differ. We will look at a lot of components over time. Just remember where to find them.
![The Unity Editor](/img/UnityInspector.jpg)

The “Scene” view is your portal to viewing you current Scene. Here you move around freely and manipulate the objects in your scene using “Gizmos”. To move around in the scene view you need to remember three shortcuts: 
*Alt + Left-click* Drag to rotate
*Alt + Right-click* Drag to zoom
*Alt + Middle-click* Drag to pan the camera
![The Unity Editor](/img/UnityScene.jpg)

Once you select and Object using left-click a *gizmo* will appear. The default should be the “move” gizmo. Hover over one of the axis and left-click-drag to move the Object along the selected axis. There are also tools for Rotation and Scale. To switch between the three you could use the buttons on the upper left toolbar. But you shouldn’t. Use the Shortcuts:
W - Move
E - Rotate
R - Scale
{{<expand>}}
If you wonder how these shortcuts come to be. Why not “R” for Rotate? Because it’s convenient for heavy users. As your thumb will always rest on “alt” for navigation purposes, you will have quick access to the main tools for the editor.
Also this corresponds to the Industry-Standard keyboard shortcuts many users know from Digital Content Creation Packages like Maya or Houdini.
{{</expand>}}

There is also an alternative way to move around the viewport. If you hold down the right mouse button four squares will appear. Now you can look around by dragging the mouse and move around using the *WASD* keys. You can try both navigation styles and see which one fits you best.


### Introducing the Bauhaus
When I started writing this “book” I asked myself, what kind of “sketches”or projects I should create. Working in 3D is a complex manner and most of the time relies on external assets. But some of you may not have the possibility to download and install them. And while many readers probably have some knowledge about how to create 3D assets themselves I really don’t want to rely on that. So what to do? Well, the answer was actually just all over the place. 2019 - the year I started writing - happens to be the “Bauhausjahr”. Or the year which marks the 100th birthday of the Bauhaus movement. And while the Bauhaus surely isn’t that easy to pin down and I am not an art historian by any means there were things to extract for this book.
They focused on reduction to simple shapes and are popular for their *Triangle, Rectangle and Circle* logo. All shapes we can easily create in a 3D Software. Most of them come as “Primitives” in a 3D package. Even more so, every shape in 3D is based upon triangles! This extreme geometric reduction is also often based on patterns and structures, things that are easily recreated using some basic math.
And while all of this was convenient, the thing that I think to be most important is the idea of experimentation. Many of the teachers at the Bauhaus encouraged their students to experiment. This spirit I’d like to pass onto you. With all the things we create, play around, try things, break things. It really is the best way to learn these things. 

### Homage to the Cuboid
One of the teachers at the Bauhaus was Josef Albers. 
History Albers
In his book “Interaction of Color” he describes how he had students collect differently colored pieces of paper and combine these by layering them on top of each other. The idea was to help students understand how they interact and how they most importantly change their appearance based on the colors beneath them. This culminated later in his paintings “Homage to the Square”. (Look it up!)
This idea will follow us through out this book. It will allow us to work quickly, iterate quickly and experiment as much as we can with one simple idea. I also think the idea of having to deal with such a simple sketch is great, because it forces you to become creative and really iterate and think about what else is possible to based on this idea. It will also work well with coding and you don’t have to install or download anything besides Unity. So I hope you enjoy playing with this as much as I do.

### Other sketches
Now I know that there are many people who are not so much into the Bauhaus. And to be honest, while I am fascinated by their ideas, there are many works I don’t really “dig” that much as well. Thus for each chapter I will try to create an alternative project for you to do. Of course, the best thing is to check out both! But for these alternative sketches it could be, that you are required to download assets. All of them will of course be free.

### “Homage to the Cuboid” in Unity

Image of the final Cuboid!

So in this chapter we will create our own “Homage to the cuboid” as shown above. As you can see this will be a rather simple thing to create: In essence we need five cubes and scale an position them properly. But we will also need a material for each of them. And we need to place our camera properly.
But first things first. Create a new scene using “ctrl + n”. You can delete everything from the new scene excet the camera. This will change the background color, as the light Unity considered to be the sun will be gone. We will deal with this later.
Next create two cubes. You can do this by either creating them form the Menu: “GameObject ---> 3D Objects ---> Cube” or by doing a “right-click ---> 3D Objects ---> Cube” in the Hierarchy view. In the inspector make sure the Translation and Rotation for both cubes are set to “0”. We will then use one Ube as a reference for a perfect cube and the other on we will squash down using the scale tool. I scaled it down to have a scale of “0.1” on the Y-Axis. You can then duplicate this cube 4 times. You can do this in the hierarchy or just press “ctrl + d”. 
Then just move them apart to liken the image above. If you want to do it more mathematically you need to go up and down in steps of “0.225”. Once you are happy with your result, you can delete the reference cube. 
Now we are missing color. Our cubes are black, because we deleted the only light source in the scene and we actually don’t want to bring it back! We will use so called “un-lit” shaders for now, as they will allow us to just pick colors perfectly. These colors will not be affected by light and will be more appropriate for our Josef Albers like studies. 
To create a material that works fur us, create one from the “Assets” menu or simply in the project view using “right-click ---> create ---> Material”. After naming the material we need to change to the before mentioned shader. In the inspector find the dropdown at the top, that says Shader. In it navigate to the “UI ---> Unlit ---> Transparent” Shader. You will be faced by many options, but we are only concerned with the color. Choose one by clicking on the color field.
GIF
You can then duplicate your materials and choose one color for each cube. To apply the materials to the cuboids you can simple drag and drop them onto the cuboids in the hierarchy or directly onto the object in the viewport.
Gif
Finally we will have to adjust our camera to match the example above. If you have Gameview and Scene view open directly next to each other you can try to push the camera where you need it. But actually that alone won’t work, because I chose an orthographic view for my sketch. The orthographic view will render all lines in parallel and thus will ignore any perspective. I thought this might work better for our Bauhaus Homage. To change this, simply select the camera and select “orthographic” from the projection dropdown. And while we are here, we can also change the background color:
Set the “Clear Flags” to “Solid Color” and then select a Color of your choice. I went with a dark grey. And you’re done!


### Project 1 - Bauhausian
Right now your focus should be to become familiar with the Unity editor and how to navigate in the 3D View, if you  aren’t already.
Because you are limited to basic shapes out of the box, you could try to recreate one of the famous Bauhaus paintings. Many of these just use simple shapes, like cubes and circles. You can just use any of the 3D basic shapes as replacements for their 2D counterparts.
Due to Copyright issues I won’t put my recreations here, but I think Q1 Suprematistic by Lazlo Moholy-Nagy could be something that is easy to recreate. You could also try to recreate the “Stacking Tables” by Josef Albers. With these you could also try to create a hierarchy inside the Hierarchy view using drag and drop. This will become handy later.

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
