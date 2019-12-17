### Disclaimer
So before we move on I just want to get a few things of my chest. I AM one of the people who way too often thought about technical stuff before design. I fell into that pit in almost any project again and again and I still have a hard time not letting those things get in the way of my design. This also means: I am very likely not at all an expert on design and how to apply it. So what follows are merely the basics and you should find input from sources who focus just on design and don't have their eyes clouded by fancy tech stuff.



### The Generative Design pitfall
This book claims to be about "Generative Design" and with such about Design in general. And that actually is a bold claim and one I am reaaaaly, really uncomfortable with. While it's one thing to tell you how programming works, design is a whole different beast. Programming is based on rules. And rules are easy to describe and put on paper. If you forget to put a semicolon in the right place your program won't run.
Design on the other hand let's you create the most outrageous crap and won't tell you at all. Even worse, stuff I would think of as outrageous crap other people actually LIKE. There are no hard rules about right and wrong. And the "rules" that actually apply are fluid and evolving. The ideas at the Bauhaus, while interesting and great to study surely can't be enforced as rules or our surroundings would be boring and bland.

So now that we know that design is hard, hard process let me tell you: Generative Design is even worse. While creating with code your logical mind is in the works all the time, and it really just cares about the code and making things work. And once you check your design and you wake the left side of the brain, it will be all sleepy and say: "Say, yeahh I guess, I guess not...", but the right side is already all over the place going crazy, just because it works. And believe me I've been there. Lots of times!
The downer comes once you show it to people and they say: 'meh'. They can't see the code. They can't see the hours you spent learning about loops and functions. They can't see the time you spend fixing bugs. And sometimes they can't see this beautiful mathematic idea at the heart of your code. They can't recognize that. And it's not their fault. It just means that the visual output you just spend hours on is just not that good. (And I think that is how WordArt came to be in the first place. Programmers creating crazy rainbow colored Fonts, just because the could.)

### Design principles
So to avoid these moments as best as we can, we will talk about design principles and how to apply them. 
The most important thing is, that principles are not rules. You can't enforce them and you shouldn't. But knowing about them helps a lot, because now you can try to teach you right side of the brain to look for some ideas it can recognize as well, while your left side of the brain get's the time to actually wake up and have it's say.

### Iteration and Formstorming

### The Frame and Formatting
Framing and Composition can be interchangeable terms, but in the context of this book I wanted to talk specifically about the frame first.
When you start a painting your work is typically limited by the size of your canvas. When you start sketching frames for a storyboard you typically start with creating a frame. Why? Because every creative decision is based on these borders. How else could you define if something is centered? 
Well... the digital world this isn't so simple anymore. Webdevelopers know exactly what I am talking about. Every website must look good in a variety of formats: Your smartphone, your Laptop as well as the good old CRT monitor that mystically runs in some places.
But worse: Consider the smartphone. In horizontal mode you are probably dealing with a 16:9 ratio, in vertical 9:16. Some manufacturers started creating 21:9 displays. With the foldable phones at the horizon, we are back at a 4:3 aspect ratio again, as well as the 16:9-ish ratio in folded mode. All in one device! And while your Laptop may as well sport a 16:9 aspect ratio, resolution and viewing distance might widely vary, again requiring dynamic adjustments to the proportions in the frame, especially if you are dealig eith type.
Unity will allow you to support all theses aspect ratios and resolutions. At it heart it really, really doesn't care where it put's it's pixels. And yet it allows you to enforce some rules. You only want to support 16:9 ratios? Done!
So you should think about how you deal with this. Where and how do you plan to publish your work? On screens in an exhibition, or maybe projected onto a wall? Or will it be a mobile app people will enjoy on their phones? Are you planning to just release on web?
To define your Unity Canvas, Unity provides a dropdown menu in the GameView. 
TODO INSERT SNAPSHOT.
Provided are some common formats like the ones we just talked about. 16:9, 16:10 or 4:3. You can click the "+"-button at the bottom to add your own aspect ratio or resolution. Once added, you can select it, and the camera should instantly switch to that aspect ratio for preview.
TODO CHECK HOW TO FORCE ASPECT RATIOS
For now I would just choose one aspect ratio for each sketch you create and ignore the problems that arise form having variable aspect ratios as a problem. Once you have an app or program that has to be deployed to devices with unknown aspect ratios you can start considering how to deal with these problems.

{{<expand>}}
### VR and AR Applications
Unity allows you to create  Interactive, Virtual Reality and Augmented Reality experiences. All of them force you to think in a completely new and different way about composition, as the viewer himself now, will create the composition. He will decide where to look and where to put his focus and interest. And while in VR you can at least create the whole world around the user, in AR you have to at least consider the user standing in a completely distracting environment. Your storytelling in these situations has to be fantastic, as this will be the driving force in leading the user through experience.
{{</expand>}}


### Composition and Balance
Composition is the art of placing your elements in the frame of your work. It's about leading the eye of the beholder and making sure the alignment of elements supports the message you try to convey with your work. While you can show the same
Write something useful here


### Balance
Balancing is all about creating
Symmetrical, Asymmetrical, Radial

Rule of thirds

### Basic shapes point, line, plane
- Absract forms
- Schnittkanten

### Contrast
Size, form, Color, Ton, Saetigung

### Structures and Relation
- Relation to one another
- Formal and informal structures
- Circular structures
- wave like structures
- spirals
- visual distribution
- invisible structures
- organic structures
### Relationen

### Textures
- visible structure

### Animation
- repetition
- frequency
- rhytm
- form
- size, color, direction, texture, mirroring, rotation around, rotation around ones own axis
- scaling, skwing, bahn
- refelctive bodies

### Color
### A word on color
- we now have an animated Version of these squares, but Josef Albers was obviously concerned with colors in these things
- at the Bauhaus he sure wan't the only one, Johannes Itten as well
- Before them Goethe took a shot at Color theory
- while they had their problems, to fix the rise of the screen comes with it's own very specific set of problems
- with this also came complex ideas like Gamma Correction and Linear Light
- it also came with color spaces 
it even got worse, if you design for the screen you essentially design for Your screen! 
Even if you have to the perfectly calibrated monitor, your enduser does not.
Their Computers come with stuff like "Night Light" which shifts colors towards red at night
The world of Color is imperfect!
The world of Color is also very, very subjective! They are changed by cultural background and personal preference. A color scheme that resonates strongly with one person might not so much with another person.


- Color Wheel
- Color combinations
- where to inspiration (nature)
- good color is hard to master and is learned by experimentation

Designers which I think work great with color:
[James Turell](http://jamesturrell.com/work/type/)
[Color Lisa](Colorlisa.com)

### Projects