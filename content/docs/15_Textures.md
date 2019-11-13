# 15 - Textures
Textures and Shaders are a tightly intertwined concept, as textures are actually additional information the shader processes to calculate the final pixels. To provide this additional information 2D images are wrapped around an 3D object along it’s UVs. These UVs are either standards defined in primitive objects, or need to be predefined in the 3D software that created the object in the firstplace.<br>
Once the textures are applied they can define a whole range of information. Simple Unlit Shader will just use the color information. “Physically Based Rendering” shaders use different textures to also affect how reflections are looking, to add faked depth detail in the object or even define areas that are supposed to be emitting light. Textures are a major factor in creating photorealism. But they are also what creates the beautiful hand drawn styles you see in some games.<br>
But! Textures are a thing we pretty much only import into Unity, the creation process for the most part is handled in other software. Thus we will only concern ourselves shortly with the most important texture slots and then move on to shaders.

### Textures
To use textures in Unity we first need to import them. Then create a material and apply it to an object. If you select the material in the Project View, you will be show all the possible inputs and settings has.<br>
Image here
To every input that shows a small rectangle in front a texture can be applied. These vary based on the Shader you have selected on the top. We will discuss the standard shader.<br>
The first input presented to us is “Albedo” and it defines how much diffuse light is reflected from a light source. Thus you will also hear the term “diffuse” used interchangeably with albedo. You can essentially  think of it as the base color of the material.<br>
The next texture we can define is “metallic” and it defines what it says: how metallic the material will appear in the rendering. Why would you want ro define that? Something is either metal or it isn’t, right? Well think of a piece of metal that has some dirt on it. The plate is metal, the dirt isn’t and thus it should not reflect like metal.<br>
Normal Map is next. Normal maps are super interesting. You will instantly see, that they have a weird look to them. What they do us, define the direction light is reflected per pixel. They are used to add fakes deoth detail to objects. They can also be used together with Height Maps. Which will increase the effect even further.<br>
Occlusion Maps define how much indirect light you objects should receive. Because Light can not be calculated accurately at run-time for such light sources, these pre-calculated maps will prevent from bringing light to areas that should not receive such strong lighting.<br>
If you check the box for Emission, you can also define a texture with information for which parts of the mesh should emit light. <br>
So how and where do you get such textures? Albedo or Color for unlit materials can be easily created in any painting map. PBR textures are typically created directly inside your 3D content creation software or in specialized texture creation tools like Substance Designer. But there are also many websites that provide these textures for download. Great websites to explore are listed in the additional resources for this chapter.

### Sprite Animations
Now textures are mostly used as static set up once and forget about them things. But there are also a few more things we can do with them. The most important being sprite animations.<br>
Sprite animations are typically used in 2D games and are more like a special kind of texture. You will probably know them from games like good old Super Mario. But you can use them in a 3D context as well. Yet they can’t be applied to 3D objects. <br>
To use sprite animations you first need a sprite sheet containing your basic animations states. They can look something like this:
Image here
You import thses just like any other image, but now you need to change their setup in the inspector. Here you can change the “Texture Type” from “Default” to “Sprite (2D and UI)”. This will change the UI shortly and now you are offered different settings, the most important being “Sprite Mode”. Set this to “Multiple”.  On the right side you will find a button to open the “Sprite editor”. This will allow you to “slice” the texture into a several animation frames. To do this click the Slice button in the topbar. You can try the automatic mode for slicing the sprites or manually set a grid. The latter is useful if you know exactly how big each piece is supposed to be. Click Slice and check the project view. Here you should see a lot of separated images.<br>
Now we need to convert this into a working animation. To do this, you can just create a new animation clip, like we did in the chapter on animation and then select all the individual frames and drag and drop them into the animation clip timeline. Unity will then automatically create a keyframe for each frame. The order in which Unity slices such textures is from left to right and then from top to bottom.<br>
You kan now just drag and drop this Sprite into the scene and Unity will automatically start playing the animation once you enter play mode. You will realize, that any sprite animation you pull in there will become it’s own Gameobject and thus can be made into a prefab. So you can reuse them in any way you find suitable.
Create some code for fancy Texture animations here


### Render Textures
But there are more fun features to the world of Textures: RenderTextures. Render Textures are textures that are textures that are created by actually rendering the scene with a camera. They can then be used like any other texture. You could use them to create effects like portals to other worlds. They are also useful to create somethink like streaking effects. Let’s look at both worlds.<br>
The first step is to actually create a RenderTexture in the ProjectView. Next we need a camera that renders TO that RenderTexture. Create a camera and in the inspector drag and drop your texture into the Render texture slot. Now you can drag the Texture onto any Gameobject in your scene and you will see the picture recorded by that camera on it. <br>
But now both cameras render the same scene. We can adjust this using RenderLayers. All objects in Unity reside on a specific Layer. Usually this is the “Default” Layer. How appropriate. No you could have some Object in you main scene and some other object on a different Layer. To create a new one, just select the Layer Dropdown menu on any object. The last entry is for adding a new Layer. All objects you want to render exclusively in your RenderTexture camera then need to be set to this Layer. On the RenderTexture camera it self you need to adjust the “Culling Mask”. The culling Mask is by default set to everything, but if you select a sepcific later, only that layer is rendered by the camera.<br>
Now depending on your need you might want to adjust the cameraflags as well. If you set this to “Don’t Clear”, the RenderTexture will contain the image you rendered just the frame before. Objects that are visible in the camera will then overwrite the pixels in which they are visible. This can have some interesting effects.<br>
More often you will probably use “DepthOnly”. This will result 
This needs more mork and use case examples

### Webcam Texture
Unity also allows us to grab the video feed of an attached webcam as input. This must be handled via script.

- Pixel Sorting / Manipulation
- Getting a Webcam texture as Input
- 




Textures - some paid some free:
https://texturehaven.com
https://textures.com
https://quixel.com/megascans/library

Texture Creation:
https://www.substance3d.com/products/substance-designer