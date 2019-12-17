# 13 - Animation
Animation is huge topic. Animation can be about bringing characters to life or about just creating a pleasing transition between two pages in app. Animation can be about huge strides and yet shines when the most subtle feelings of an character

Philisophical shit about Animation

### Animation in Unity
Using Unitys Animation System can be utterly simple, but also scales very well into extremely complicated Animation of Characters and blending between Animations based states. If you are familiar with Animation systems in other software like After effects, Maya or Blender, you are probably used to just selecting an object and being able to add Keyframes. This doesn't work in Unity.\
Animations in Unity come with two components: An Animation Clip a.k.a the actual animation and an Animation Controller. The Animation Controller can handle multiple Animations and switch or transition between Animations.\
While this might seems complicated in the first place, it's actually a fantastic system. It makes all your animations easily reusable. Once set up, you can use it over and over again on any object that has the same components applied to it.\
You also don't HAVE to concern yourself to much with the animation controller when starting out, because Unity can handle it's creation for you. And as classics are always a good way to get started: Let's create our first bouncing ball!\
To get started just add a Sphere to the scene and zero out it's transform. You can also create Cube as a floor to bounce around on. Next we need to open the Animation Window: "Animation ---> Animation Window". With the Sphere selected the animation window should offer you a button to create an Animation. Animation clips are actually physically saved as individual objects on your Hard drive. You could copy them to a different project, if you wanted to. Talk about re-usability!\
If you create Animations this way Unity will automatically create an Animator Controller as well for you and apply the Animation. So you really don't have to care about it for now, yet you will find it applied to the Sphere.\
To start animating, we need to add Properties we want to animate. Once you click the button you are presented with all the components that are currently applied to the sphere that actually have properties that can be animated. From the transform component go ahead an add the Position and Scale parameters using the "+" icon.\
Unity will by default create an animation that does nothing and is one second long.\
To change the values drag the playhead to the position, where you need Keyframes and add them using rightclick. You can only change the values of keyframes that are at the position of the Playhead. If you want Unity to automatically set keyframes while editing, press the little red recording button. Because you can easily make mistakes in recordig mode, the timeline head will turn red, as well as the values in the inspector. You can also use the gizmos in the editor to animate your object.\
While Unity will create some default interpolation for us while adding Keyframes, it's very likely that we want to tweak them. In the lower bar of the Animation window you can switch between the Dopesheet and the Curves view. For finer control over you animation the Curves view is an indespensible tool to create great animations.\
Unity will show you the interpolation curves it created for you and you can just go ahead and grab the Keyframes. Using the handles you can adjust you interpolation between the keyframes. If you need hard changes in your animation you need work with broken handles. to switch the handle types, just select the Keyframes you want to affect and press select the type you need using the righclick menu.\
While you can always go in and and preview you current animations using Animation window, you also just switch to Playmode. The way we created the animation, Unity has set this up for us as an looping Animation.\
So here is the result and the curves for my super simple bouncing ball:
Todo Bouncing ball and curves
{{<expand>}}
If you are completly new to animation and want to get into I suggest looking up "The Animators Survival Kit" by Richard Williams. "The Illusion of Life" by Frank Thomas and Ollie Johnson is another great book to look at. They first introduced the "Twelve principles of animation". To get an overview you can also do quick search on YouTube.
{{</expand>}}
Because animation is hard work, Unity has at least some shortcuts set up for us, to make our lives easier:
|Shift+Comma|First Keyframe|
| ------------- | ------------- |
|Shift+K|Key Modified|
|K|Key Selected|
|Shift+Period|Last Keyframe|
|Period|Next Frame|
|Alt+Period|Next Keyframe|
|Space|Play Animation|
|Comma|Previous Frame|
|Alt+Comma|Previous Keyframe|



So now that we know how to actually create Animations, let's look at how they are actually set up and connected on the gameObject itself.\
If you take a look at your sphere, you will see, that the component that's actually applied to the sphere is an "Animator". \
The Animator is responsible for handling the Animation of your object and requires and Animator Controller to work. You might think this is an unnecessary step, but it is also handling things that only become relevant in more complex scenarios, like applying Root Motion. (Try it, it's fun.)\
The first parameter the Animator supplies is a Controller. Right now that's probably named "Sphere". Or if you have renamed your Sphere before creating the Animation, it's probably named like that. If you double-click that Controller Unity will jump to the Controller in the Project View. It should be in the same folder as the Animation Clip you created. Double Click on that and the Animator Window should pop up.\
Here you will see a left side with an entry called Base Layer as well as a Blueprint like view with three elements inside. This is a "State Machine". It handles in Animation the current object is currently in, and if and how this object can transition to another "State". \
By default you be presented with three states. "Entry", "Any State" and a state named after your Animation Clip. The Entry State will be linked to your animation clip. This shows you that, as soon as the object becomes active the animation clip will be played. If you switch into PlayMode, you will see also see progress bar appear on the State that is currently playing.\
Go ahead and create a new animation clip, or just duplicate the one you have. You can drag an drop it in to the state machine as well. As you will it will not have any connection by default, so we need to set it up. Select either one of the Animation clips and go "RightClick ---> Make Transition". And then click on the object you want to transition to. If you want to be able yo switch been both animations, you have to create transitions in both directions. Switch into playmode to see all of this working.\
Now depending on the animation you have set up, you might notice that your animations look sluggish. The first time i did this I got really confused, about what happens. Because this whole system is set up to also manage Characters and these states could be things like jumping, running or sitting, Unity by default applies a blending operation between the states.\
To see this select one of the arrows a.k.a transition and check the inspector. Here you will see a transition timeline. If you move the left arrow on the playbar directly next to the right one, you will be able to move the lower clip to the right as well, and there will not be any transition blending.\
If you have a transition selected in the inspector you will also get a preview window at the bottom of the inspector. here you can view the transition and make adjustments to it, if that's necessary.\

### Typical Animation Transitions
Okay, all of this a lot of stuff to just get some animation rocking. And this certainly could use some finger practice. So before we move on into scripting Animations, let's play with our Homage to the Cuboid again.



The beauty of LateUpdate()

### Projects
