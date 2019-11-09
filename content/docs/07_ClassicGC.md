# 07 - Classic CC Techniques in Unity
If you came here as someone with a background in Processing or p5.js, you might be missing some very common processing techniques, that aren’t too obvious to recreate in Unity. The first thing being the complete handling of the background. In Processing you would handle this in the initial lines of code of your script. In Unity all this functionality is tied to the camera. We will look at setting this up in the editor first. But of course all these things are available via code as well.
By default Unity will clear the complete Render Buffer each frame and render the default skybox as a background for your scene. The skybox obviously isn’t the most useful think when you want to create non-enviromental scenes. The most basic alternative to this is setting is a solid background color. 
![Setting the background to “solid color”](/img/UnityCameraBackgroundSolidColor.jpg)
This will clear the image buffer with the selected solid color in the field right below the clear flag. As mentioned before, you can of course access all of this via script as well.
{{<highlight c>}}
public class ShapeLerp : MonoBehaviour
{
    public Camera myCamera;
    void Start()
    {
        myCamera = Camera.main;
        myCamera.clearFlags = CameraClearFlags.SolidColor;
        myCamera.backgroundColor = Color.white;
    }
}
{{</highlight>}}
This of course means, you could also change or animate the clear buffer color to your liking.
Shape Lerper Example here

Another very popular type of clearing the background is: not clearing. This means the previous rendered frame will stay in the renderbuffer and will only be overwritten in areas the camera deems worthy to behold. What’s worthy? The camera has a settings for near clipping and far clipping. Anything closer that near will not be seen by the camera, everything farther than the far setting will be ignored as well. This range is necessary to make computer graphics feasible. 
{{<expand>}}
Why is it necessary?
Think of one meter of distance. How far can we break this up? One meter is 100 cm, or 1000 Milimeters, or 1000000000000 picometers. Femtometers anyone? And now Consider Femtometers at 100km distance.
Our Computers just can’t handle such values very well, and even more importantly: not efficient.
The solution? Define a range the camera sees and split value we actually can hold in one piece of memory over that range. The larger the range, the less precision we actually get. But most of the time that works out just fine.
{{</expand>}}
Built upon the idea of not clearing the render buffer are built many Processing sketches which involve random Walkers or painting like applications. The main piece of code we need to concern ourselves with is this:
{{<highlight c>}} private Camera cam;  void Start() {     cam = Camera.main;     cam.clearFlags = CameraClearFlags.SolidColor;     cam.backgroundColor = Color.white;       }  void Update() {     if (Time.frameCount > 2){         cam.clearFlags = CameraClearFlags.Nothing;     } }
{{</highlight>}}
We create a variable to get hold of the Camera in our scene and assign it using `Camera.main;`. Next we set the clearFlag of the Camera to Solid Color and assign white. We could have done this in the editor as well and if you assigned a background color on the camera it will be overridden by our code. Be aware of that.
In the `Update()` method we simply wait for 2 Frames before changing the CameraClearFlag to nothing. From this point forward we keep the Framebuffer and can override it.
{{<expand>}}
Other Options?
Of course you could solve how to create the initial background completely differently. You could have a Plane with an image on it and destroy it after two Frames, or just move it out of the way. 
{{</expand>}}
But to prove our point let’s recreate another very popular Processing Sketch: The Random Walk. The idea is, to have an Object, often the mere size of a pixel, grab a random number and based on it decide in which direction to move next. 
{{<highlight c>}}
public GameObject WalkerPrefab; private GameObject Walker; private Vector3 movementDirection; public float movementDistance = 0.1f; public float walkerSize = 0.1f;
{{</highlight>}}
This is just the code for setting things up. We have to create variables for size and movement distance, because we are once again not dealing with pixels, so we want the creative control in the Unity Editor.
{{<highlight c>}}
Walker = Instantiate(WalkerPrefab, Vector3.zero, Quaternion.identity); Walker.transform.localScale *= walkerSize;
{{</highlight>}}
This is nothing but the typical initialization of our object in the start function. The interesting part obviously belongs into the Update method:
{{<highlight c>}}
int randomNumber = Random.Range(0, 4); if (randomNumber == 0) {     movementDirection = Vector3.up; } else if (randomNumber == 1) {     movementDirection = Vector3.right; } else if (randomNumber == 2) {     movementDirection = Vector3.down; } else {     movementDirection = Vector3.left; }  Walker.transform.position = Walker.transform.position + movementDirection * movementDistance;
{{</highlight>}}
To implement a simple random walk we just generate a Random integer between 0 and 3. Note that the second argument to Random.Range() is exclusive, so we have to add one to it. Then we just define the movement direction based on the random number.
Lastly we just add the movementDirection to  the current position and assign it. The movement Distance is for us to get some creative control over the outcome and ist most likely tied to size of the Walker we crated.
So this is what we got so far:
IMAGE OF RANDOM WALKER WITHOUT FADE
If you let it walk for a while, you will realize, the walker will sooner or later leave the bounds of the frame. This means we need to decide on way to deal with this. 
Consider edgecases, what happens out of bounds
Next we need to find a way to fade the old frames out over time. In Processing the background takes an Alpha as argument and thus is then written on top of the framebuffer. In Unity the alpha of the background color is just ignored. This means we need to create a transparent front layer ourselves.
To do so we create a simple plane just in front of the camera. For the plane we need to create a special material, which is configured to properly override the render buffer: The “Sprite > Default” Material will do the trick just fine. Interestingly enough the alpha value we would want to set is `7`. Everything lower than this value will result in not fading out all values properly. But this value was also supposed to be the value to control the speed of fading. To get even more control over the speed of fading we can write a little script, which will enable and disable rendering for the plane in a certain interval.

3D Scanner Effect
3D Random Walker
Random Walker with traces that draw shapes - Random Walker to show fading away stuff over time

### The Fading Paint Effect
Another very popular thing in Processing is to have some kind of Paint effects or even fading paint effects. In the 2D focused world of Processing, all of your shapes are drawn on a plane. This Plane is defined by Pixels. So it is very reasonable to just name the Pixel at whose position you would want to i.e. draw a circle. In Unity on the other hand we are dealing with 3D Space, which means we have to also think about the Z-Axis or the Depth of things. This makes the process somewhat more complex, but will also give us some interesting possibilities to play with.
The key to solving this is to shoot an in invisible Ray starting at the camera Center through the Position of our mouse in ScreenSpace. If this Ray is hitting some object, we can retrieve information about the object we hit as well as the hit itself. Most importantly for us, the position at which we hit something.
To put this into practice we need to actually hit something. This something will be a plane we position directly adverse to the Camera. We also need to scale it big enough to fill the area our Camera can see. We will then add a Rigidbody Component to it.
![Camera facing Plane for Raycasting](/img/UnityCameraFacingPlaneForRaytracing.jpg)
The intial setup is very similar to our setup for creating the fading random Walker. We just add some variables for our brush.
{{<highlight c>}}
public GameObject brush; private GameObject currentBrush; private Camera mainCamera; // Start is called before the first frame update void Start() {     mainCamera = Camera.main;     mainCamera.clearFlags = CameraClearFlags.SolidColor;     mainCamera.backgroundColor = Color.white;      currentBrush = Instantiate(brush, Vector3.zero, Quaternion.identity); }
{{</highlight>}}



TODO: We can also do this with code: Code


Scanner Effect on a 3D Object which draws shiny/neon spheres








