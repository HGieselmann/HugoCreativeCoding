# 17 - Audio
"Audio is 50%!". I don't know how often I heard this sentence over the years yet. And yet it surly isn't wrong! Audio adds a completely new layer to the works you create. And for some cases I guess you could argue "Audio is even 60% of the experience!". While you can easily close your eyes or look away, you can't so easily block out all the sound that's around you. \
Write more on the importance of Audio

No that we have established the importance of audio in our projects, let's look at some of the things we need to take care of, when dealing with audio in Unity. In comparison with cinema, audio in a interactive 3D world can't be just layed out perfectly in one Audio track. Left and Right now isn't based on the screen you look at anymore, but based on the view-axis of the camera in 3D space. If we try to convey a realistic experience, we also need a way to increase volume as soon as we come closer, and slowly fade it away while the camera departs from the source. \

Luckily enough Unity makes the process of setting these things up very convenient. To set it up in the first place, all we need is an "Audio Listener" and an "Audio Source". The Audio Listener component comes pre setup with every scene you create and is attached to your camera. You only really need to think about it, when you deal with multiple cameras in your scene, because only one Audio Listener can be active at any given time. It has so settings to take care of and can only be turned on and off. So that's nice! \
TODO Image of Audio Listener on Camera
The Audio Source component on the other hand is a little more complex:
TODO Image of Audio Source on 
The first thing you will need to supply to your Audio Source is an actual AudioClip. To add an AudioClip to your project in the first place, you can just drag and drop an AudioFile into your project view. Or use "RightClick ---> Import New Asset..." in the project view. Then just drag an drop it into the AudioClip on your Audio Source component. If you now go ahead an enter Play mode, you will immediatly begin to hear the AudioClip you added. This works, becuse "PlayOnAwake" by default is active. You will also find some settings that will be immediately obvious: Loop, mute, pitch and Volume. Bypassing effects should be pretty much self explanatory as well. \
This all becomes more interesting once you push the Spatial blend slider all the way to the right. This will activate the 3D Sound settings you find below. To test this out, make sure your camera and Audio source are in the exact same space in your world. Then enter Play Mode and you grab your camera and move it around in the scene, while the scene is playing. You should hear the Audio Clip fading away with distance. \
How harsh this falloff will be can be defined in the curve below. The predefined Logarithmic Rolloff is how sound would react in the real world. If you want a more artistic approach to your Audio, you can switch this to a Linear falloff or even create a Custom falloff. \
If you are not yet an audio nerd it is probably a good idea, to just play around with these settings to get a feeling for what they actually do. You can even add on Audio effect components like Echo and Reverb. I will not go over these in detail, as audio and audio effects are a huge topic in themselves. But remember, that all of these effects have to be calculated at run-time. So if there are Audio Clips that i.e. always have to to be distorted, it's better to apply such effects in an external program before even importing this into unity.

Now that we have established how audio is handled on basic level inside Unity, let's look at handling audio in a real-world scenario. I guess there are two kinds of audio sources we will have to deal with regularly. One is environment audio that is played from objects in your scene constantly. Think of a tree in the wind. You would want to have it play the rustling of the leaves all the time. So it makes very much sense to have the audio source directly inside your prefab and have it looping as long as your scene runs. \
Add a tiny tree that rustles in the wind
Other sounds you probably want to manage in some way. You maybe want to change the background music or play Sounds when you click on a button in a menu. Now it would be really annoying to add an Audio Source to every button in your menu. This is where Audio Manager classes come in. \

### Singletons
Manager classes are typically an implementation of the Singleton Pattern. The idea of a singelton is, to make sure you only have exactly one instance of the class in your scene. This instance will then handle whatever needs be handled.
{{<expand>}}
### Singletons can be bad...\
There are reasons for why Singletons are a bad idea. And Robert Nystrom goes over them in great detail in his book "Game Programming Patterns". But as a beginner, as I assume you are, you can feel free to ignore that. But be aware of it and once you start bigger projects be sure to read up on this!\
{{</expand>}}
So let's look at the implementation of an generic Singleton inside Unity.
{{<highlight c>}}
using UnityEngine;

public class Singleton : MonoBehaviour
{
    public static Singleton instance;
    void Awake(){
        if (instance == null){
            instance = this;
        }else{
            Destroy(gameObject);
        }
    }

    public void Log(){
        Debug.Log("This got called.");
    }
}
{{</highlight>}}

We create a class "Singleton"  and then as first step declare a variable named "instance" of type "Singleton". Thus we store a reference to ourself. Once this object is created Awake() gets called. This most likely the moment you press play, but could be at any time during your game. Then we check if instance is already assigned. If that's not the case, we choose this object as the instance. If an instance already exists, Destroy the current which just tried to become the instance.\
Because our class is `public` and `static` we can access it from any other class in the scene:


{{<highlight c>}}
using UnityEngine;

public class Caller : MonoBehaviour
{
    // Update is called once per frame
    void Update()
    {
        if(Input.GetKey(KeyCode.A)){
            Singleton.instance.Log();
        }
    }
}
{{</highlight>}}

So this is how to setup a basic singleton.\
So how can we use this to actually manage Audio in our scene?\

{{<highlight c>}}
using UnityEngine;
using UnityEngine.Audio;
 
public class AudioManager : MonoBehaviour
{
    public static AudioManager Instance;
 
    public AudioSource Music;
    public AudioSource Sfx;
 
    void Awake(){
        if (Instance == null){
            Instance = this;
        }else{
            Destroy(gameObject);
        }
 
        Music = this.gameObject.AddComponent<AudioSource>();
        Sfx = this.gameObject.AddComponent<AudioSource>();
    }
 
    public void PlayMusic(AudioClip musicClip){
        Music.clip = musicClip;
        Music.Play();
        Music.loop = true;
    }
 
    public void PlaySFX(AudioClip sfxClip){
        Sfx.PlayOneShot(sfxClip);
    }
}
 
{{</highlight>}}

As you can see we just recreate the same pattern as with our basic Singleton. The rest of the class deals with actually playing Audio. We create an AudioSource for background music and one for sound effects we might want to play. We then create a function for each of them. The difference between the two functions is how we actually play the Audio.\
In the PlayMusic() method we set the music clip and then use the `Play()` function to actually play the clip. \
In the PlaySFX method we use the `PlayOneShot()` method. The difference between the two is, that we can fire multiple sounds at the the same time when using `PlayOneShot()`, while we can make use of the loop feature, when having a dedicated AudioSource for an AudioClip.

So how do we call this?
{{<highlight c>}}
using UnityEngine;
 
public class Caller1 : MonoBehaviour
{
    public AudioClip SoundFx;
 
    private void Update(){
        if(Input.GetKeyDown(KeyCode.A)){
            AudioManager.Instance.PlaySFX(SoundFx);
        }
    }
}
{{</highlight>}}
This pretty much straight forward, as we just call the function on the Audio Manager. The only thing you have to note, that we store the actual Audio Clip on the caller. The manager is just responsible for playing the Audio, which Audio to play is in the responsibility of the object that is calling the Manager.

Talk about Audio Mixers?? Rly?

### Projects
- Generative with Audio playing, reacting
- Audio Visualizer
- Multiple Audio Input for better Music Visualization
- 

