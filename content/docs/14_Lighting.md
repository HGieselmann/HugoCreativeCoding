# 14 - Lighting
For creatives light is super essential as soon as you leave the strictly graphical world. Light plays an important role in setting the scene and defining the mood. Think of the warm soft lighting during sundown at the beach, or a a dark alley only lit by a lone flickering streetlamp. The Lights alone can define the feeling we get, once we look at an image. The same scene in different lighting can tell completly different stories.<br>
create some examples here
### Light Sources
Unity provides you with several different light sources to create beautiful settings. All of them can be created from the Hierachy view, or by add a “Light” component to any Gameobject. Preferably an empty one, of course.<br>
The most basic light source Unity offers is the “Point Light”, which resembles your typical lightbulb in the real world. It shines light from on center point in all directions. The basic settings in Unity from them include color, intensity and range. Range might seem a bit odd, as you could expect intensity to be the driving factor in how far a light should shine, right? Actually they both decide on that, in which the Range is a hard limiter on the distance the light is contributing to the scene. We will discuss the reasoning behind this later.<br>
Next up is the “Spot Light”. The spot lights shines in light on a very specific spot and you can adjust the cone angle to be almost 180 degrees. It also features the ominous range value.<br>
The “Directional Light” casts it rays in perfect parallel manner into the scene. It is most often use as a sunlight. And while you might argue, that the sun is a perfect example of point light, it’s distance from earth makes acceptable to simplify them to perfectly parallel in this context.<br>
The last light source in the List is the “Area Light” and it tells you right on the dropdown menu that it’s “baked only”. One could argue that every light source should be an area light, but to actually properly calculate Area Lights you would have to sample Light rays from different points on the Light surface, and that’s terribly expensive to do. (But for more on that matter: see below.)<br>

### Shadows
If you were curious enough to add a light into the scene already, you might have realized that all of the real-time lights (Point, Spot, Directional) do not actually cast a shadow by default. To enable shadows on a light you have to enable them on the Light component by choosing either of the two possible shadow types: Hard or Soft.<br>
To keep it simple: Hard Shadows may not be very realistic, but in turn they are fast. Soft shadows are slower to calculate but look much more natural. Shadows come with a few confusing settings, and directional lights even have shadows in the overall graphics settings. You only need to concern yourself with these if you actually run into problems with your shadows.

### Real-time vs baked lighting.
As in the real world lighting can be a rather technical subject as well. Maybe even more so, because the interactions of light in the real world are very, very complex and thus they are extremely resource intensive to calculate. Because of this complexity of the matter, lots of these technical details are out of the scope of this book. I will link to more advances discussions on the matter below.
{{<expand>}}
#### Ray-tracing
To be able to recreate the interactions of lightrays in the environment programmers invented a technique called ray-tracing. This technique actually shoots rays of light out into the scene an calculates how they interact with a given surface. The rays then bounce further until a light ray has lost all it’s emissive power.<br>
This is done several, several time until you finally get an image that is noise free.<br>
Recent developments in hardware have led to ray-tracing becoming available in game-engines as well, but is only available on high-end hardware. Thus we will not make use of realtime ray-tracing as of now.<br>
{{</expand>}}
To cope with these limitations in rendering power Unity offers us two essential kinds of lighting. Real-time lighting and so called “baked” lighting.<br>
Real-time lights are re-calculated each frame. To handle this, they take quite a few shortcuts in accuracy: Real-time light doesn’t bounce. Real-time shadows a pretty much sharp, or blurred in a kind of fake way. And while this sounds depreciative I am actually more then fascinated about what you can achieve visually using these fakes. Also these light are real-time. This means they can change color or intensity. They can move. They are really fully interactive, which is great!<br>
“Baked” Lighting on the other hand is created using ray-tracing (s.o.). The advantages of baked lighting are manifold. Light that bounces around a scene will create a much softer and more realistic look. You will receive proper shadowing in corners as well as soft shadows. 

#### Baked Lighting and Global Illumination
 Baking refers to actually pre-calculating how the light is bouncing around the scene and storing the information in images. These images are created and stored for each object that Unity recognizes as an “static” object. This process is done once on the machine of the creator - a.k.a. your machine - and then this high quality lighting has not be recalculated on a client machine, and thus can be pretty performant on slower machines as well.

So how do you choose the best approach to lighting? Well, you can have both! You can select Lights and Objects which will never change to be static and thus be included in the light baking process. All lights and objects that need to be able to move around or change color can be left un-static and will be rendered as real-time objects. As light is always calculated additive, both rendering ways work fine together on an artistic level as well.
Unity even provides a third option: “Precomputed real-time global illumination”. This option will not calculate Light Maps but rather so called Light “Assets”. These Light Assets store information about how Light would travel through the scene and then interact with static objects. This means the light can change at runtime and these changes will at least affect static objects in the scene.

### Lighting Settings
Now that we have some idea what actually happens in the background, let’s look at the settings themselves. The most important thing, and one that’s easily forgotten about, is actually setting all the meshes you want to be “Static”. On object you can find right next to the name a little checkbox for “Static”. All lights and all objects that are supposed to be baked, need to have this checkbox enabled. This might even trigger the background baking process already. If a loading bar appears in the lower right corner and your scene textures “pop” sometimes, that’s probably the case.<br>
To actually get some control on the creation of baked Lighting we need to check the Lighting Settings. You can access these via “Window ---> Rendering ---> Lighting Settings”.<br>
The first tab is about the Environment. Environment meaning everything Unity renders once rays don’t hit objects anymore. By default Unity has a Skybox set up for us. And in new scenes the default Directional light is here set up as sun as well, which leads to changes in horizon color when we rotate the directional light. In our topic of baking light, this horizon will lead to shadows tinted in the horizon color, as it is sampled as an emissive light source. Yet you can also change this from skybox to color or gradient.













Additional resources:
Light of the visual artist - Richard Yot
Color and Light: A Guide for the realist painter - James Gurney

Technical Discussions:
https://learn.unity.com/tutorial/precomputed-realtime-gi-global-illumination