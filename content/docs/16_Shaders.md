# 16 - Shaders
A shader is little piece of software, or a script, that tells the graphics card how to interpret the Lighting information an object is receiving and how to interpret that light. Unlit shaders can generate these informations for themselves.\
A very simple example would be a red sphere and a white light in the scene. If the light source is sending white light, how is the sphere ending up red? How it is determining the specular light on the sphere? How is the falloff in brightness calculated? All of this done inside the shader. And while we could probably wrap our head around this, things get immensely complicated once you talk about topics like reflection or refraction.\
Luckily Unity provides us a lot of pre-built shaders. We have been using them since chapter one. But while they can be very complex, they are also very powerful an interesting.\
But what if you want to create your own? I will spare you the hardship of learning HLSL (High-Level Shader Language) and introduce you to one of the more recent features of Unity:\

### The Shader Graph
The Shader Graph is Unitys approach to make Shader creation much more accessible for beginners and it also makes shader creation a visual process. Which is great I think, because I feel it makes it easier to stay in the more creative part of your mind.\
Shader Graph is a Node graph in which you can drag and drop nodes which hold mathematical operations around to create visual outputs. \
Now to set up and use Shader Graph you need to run either the "High Definition Render Pipeline (HDRP)" or the "Universal Render Pipline (URP)" (previously known as Lightweight Renderpipeline). If you have set your project up using all the defaults, then that is probably not the case. The easiest way will be to just create a new Project from the Unity Hub using either Pipeline. In HDRP you will have access to some more features, but it will also not be suitable for deployment to lower end devices.\
Once you have a new Project set up, check the Package Manager to see if you have the Shader Graph package activated. If so create a new Plane in the scene, a new material and apply it to the plane, and also create a new ShaderGraph using "RightClick ---> Shader ---> Unlit Graph" in the Project View.\
On the material you can now select the Shader Graph you just created. Now let's look at the actual Shader Graph. In the Project View "DoubleClick" on the ShaderGraph you created. An new Window will pop up. I suggest docking it somewhere in the interface and with your Mouse hovering over the window press "Shift + Spacebar". This will maximize the window. The same Shortcut will bring you back to normal view.\
In the Shader Graph you will be greeted by three windows. (If not, simply press "A".)\
The one in the lower right is your "Main Preview". It will preview the end result of your Shader. You can resize it by dragging the little Grey bar in the lower right corner. You can also toggle it on and of using the "Main Preview" Button in the Topbar.\
In the upper left you will find the Blackboard. The Blackboard holds all the parameters you want to expose to an artist in the editor.\
The last thing you will see is a "Master Node". This is the actual thing that controls the Output of your node. This Master Node also defines some of the main properties of your ShaderGraph. When we created the ShaderGraph, we chose an "Unlit Graph". This means our Shader will ignore any kind of lighting information. For a start this will be easier to deal with.\
The Master Node will accept several different Inputs. So let's start with the most obvious one: Color.\
There is already a Color selector provided, but one that's just here as an absolute basic. We want to create our own Color Node. To create a node either go "RightClick ---> Create Node" or press Spacebar. To find the color node, you can either just start typing, or go "Input ---> Basic ---> Color". Now you can connect both nodes by dragging from the color output to the color input on the master node.\
Notice the Colors on the Inputs and Outputs. They will give you information about the kind of information that is passed from a to b with the number in parentheses giving another hint.\
The pink Color that is coming from the color node is actually a Vector4. Meaning Red, Green, Blue and Alpha. The Master Node accepts a Color of type Vector3: Red, Green and Blue. (Remember this form our Coding Section?). Unity in this case will actually try it's best to do the conversion for you itself, and will just discard the Alpha, as the Master Node has a separate alpha input.\
Be careful though! If you expect Unity to use the Alpha Channel, as Alpha when you plug the Color node into the Alpha Input of the Master Node you will be disappointed. Unity will always dispose the last channel. Thus Red will be considered the Alpha Channel in this case. You see those Colors are important.\
{{<expand>}}
To fix this problem you can split and and combine channels using the split and combine nodes. Take a look at this setup. The split node splits the Vector4 in to four Vector1s. Then you can combine RGB together again. Here all lines have the same color, which indicates Unity is not doing any conversion.
{{</expand>}}
No that we have changed the color go back to the scene view and check out your plane. Is it colored? Probably not. A real gotcha with the Shader Graph is, you have to always save it, before any changes show up in the scene. And "Ctrl + S" won't do the trick. On the topbar of the Shader Graph Window is a "Save Asset" button. Once you click it, the shader will be recompiled and any changes will be visible in the scene.\
### Nodes
No let's start playing around and leverage the power of nodes. If you open up the "Create Node" Window using "Spacebar" you will see the several different Categories Unity offers and you can have a look around for yourself. I can't go over all of them, because there are ton!\
So we will just create a few Graphs and along the way I'll explain some of the nodes I find most useful.\
#### De-Saturate Shader
Our first shader will be super simple. We want to input a Texture and then be able to adjust it slightly using parameters.\
This is the node setup:\
Add Image here of desaturate Shader
As I knew that I want to be able to change the texture itself aswell as it's saturation I will create two Parameters on the blackboard. A "Texture2D" and a "Vector1". A Vector1 is essentially a float. Once created, you can create defaults and drag them into the View, so they show up as Nodes. If you hover over them in either you the Graph view or the blackboard they will be highlighted to be easier to find in complexer Graphs.\
As you will realize the output of the Texture 2D can't be plugged into the Master Node directly. You will actually tell Unity to "Sample" it using a "Sample 2D Texture" node. This is necessary to define how the texture is interpreted. Now you will see you are offered either separate channels or the combined RGBA we discussed earlier.\
You can now add the Saturation node from the Artistic category and plug in your Vector1 into the saturation input. Finally hook up the Master node and make sure to hit the "Save Asset" button.\
In the Editor you can now setup your shader in a Material, apply it and drag and drop any image into the Texture slot. You should now be able to adjust the saturation.\
#### More adjustments
You might have seen that the "Artist" category features way more adjustment filters. As you might imagine you can just hook them up one after the other, but be sure to think about the order of operations, as this might have an impact on the resulting image.\
Here is an example of a shader that allows for Color Temperature and Contrast adjustments as well.
Here needs to be a screenshot
While creating all the parameters you should make sure to set useful names for them and their reference, as well as for their defaults. Vector1 nodes for example default to 0. Plug that into the contrast node an you will get a perfect grey, completely independent of what your texture looks like... That's not a default other artists would expect.
{{<expand>}}
#### Why grey?
The Contrast node scales the brightness around a center value. If you scale all values that range from 0 to 1 to zero you returen that center value for all colors. That's grey.\
{{</expand>}}
#### Animated Noise Shader
Okay let's get things moving in our next Shader. Well also finally do some coding again!\
I essentially started with one "Gradient Noise". It creates a simple noise with values between 0 and 1. As I was aiming for a more "blob-like" structure I added a contrast node right after it and increased the contrast extremely. To make sure I was not having any values above 1 or below zero I added in a clamp node. From there split ways. The output was already perfect for the alpha, for color I added a color parameter to multiply it with.\
For the animation to appear we need a value that can create movement. You know what we need: Time! And of course there is a "Time" node. It even has a sined and cosined time value. But time alone won't do the trick, we need a node that can actually manipulate the noise. This is where the nodes from the UV Section come in. \
The first node I chose to manipulate my noise was "Tiling and offset". It automatically creates a basic UV space and will tile and offset it if you change the corresponding values. But you could also add UV map you already have in there and manipulate that.\
The problem with one noise is, it is just repeating and that's very obvious. That's why I added another noise with a "Rotation" node added to it. After multiplying both noises together the looping pattern isn't that obvious anymore.\
The last node I added was yet another Multiply after the time node. This allows for adjustments in the speed in the animation.\
The last Gotcha! is the settings for Alphas in Unity. By default all Shaders created in Unity are set to "Opaque" and any alpha will just be ignored. To change this we need to go into the settings of the Master node. On the Master node find the little cogwheel and click it. Here you have some advanced settings, we are interested in the "Surface" dropdown menu. Change it from "Opaque" to "Transparent". This should allow you to see a transparent noise in the scene. And that's it.\
Let's script this!
Scripting this shit!


Additional Resources on shaders: \
https://thebookofshaders.com/ \
https://catlikecoding.com/unity/tutorials/ \
https://www.youtube.com/watch?time_continue=1&v=9WW5-0N1DsI \
https://www.shadertoy.com/ \
https://en.wikibooks.org/wiki/Cg_Programming/Unity \