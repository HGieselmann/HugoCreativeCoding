### User Interfaces
For many of these more “sketch-like” scenes we have been creating you probably don’t need any kind of user interface. But say you want to bring them all together to show off your progress in Unity.
Or you could use Unity as way of creating a UI Design Test app, that could actually be easily deployed to Android or iOS phones.
Thus we will look at how UIs are laid out in Unity and how the script setup works. We will also get our feet wet with Scene Management, which will allow us to actually switch between scenes at runtime and even retain the User Interface along the way.

The first UI we will create is very, very simple. We will create two buttons which will allow us to switch between our scenes in a built Version of our sketches, thus giving you the option to better show off what you have created so far.

To start creating UIs in Unity just RightClick ---> UI ---> Button. 
{{<expand>}}
#### TestMesh Pro
You can probably choose between regular UI Buttons and “TextMesh Pro” Buttons. Functionality-wise they don’t differ much, yet you can do much more advanced text-styling with the TextMesh Pro elements. So if you fancy a little more advanced fonts, go for the TextMesh Pro ones.
{{</expand>}}
As you can see this probably created a bunch of elements at once. A Canvas, an EventSystem and the button itself with some text attached to it. It also created a huuuuge rectangle and a huge button in the Scene view.
This happens because Unity offers three ways to create your User Interfaces in your scene:
The first and default one - “Screen Space Overlay” -  will be overlayed on top of your whole scene at runtime and is thus displayed in pixel size in the Scene view. Press “2” to switch to the “2D” view mode to better see your UI.
The second option - “Screen Space Camera” will be rendered in a certain distance from the camera but stick to it. But camera settings like Field of View will then actively affect. This is also interesting for post processing effects. If you would want effects like Grain applied to your UI as well, then this is the way to go.
“World Space” as last option will actually render the UI in 3D Space. This could be interesting for Virtual Reality UIs or in Games where you want your character to be knowing about the User Interface as well.
We will stick to the basic Screen Space Overlay UI. As it is very possible, what we might want to add another Screen. Maybe like a Start Screen or Main Menu. So let’s parent each screen to an empty GameObject. For reasons you will understand later, we will also create an Empty GameObject and parent our Canvas Object and our Event System below.
![Hierarchy Layout](/img/UnityUIHierarchyLayout.jpg)
This way we can just enable and disable to the parent GameObject to turn of our UI or switch between UI Elements.
Now you can see I already duplicated and named those Buttons and Screens. but we also need to change the text inside the buttons. To do this we can just change the text on the text elements that are parented to each button. Here you can also some of the text styling elements. If you went with TextMesh Pro you will have a lot more options at your fingertips.
If you don’t see this properly, make sure you actually have only one screen visible at a time. That’s what our parenting structure is supposed to help with.
Next you can layout your buttons in the Scene view. Here Unity will offer you the “Rect Transform Tool” as default way of manipulating UI elements. This is really great, because it’s very intuitive. You can just use the blue circles in the corners to rescale the items and push them around. The Rect Transform tool will also show you lines when your buttons align to one another. You can also scale and move your buttons around via the inspector if you prefer to do that.
In the inspector you will now also see that you have a “Rect Transform” component instead of your normal Transform component. While you can edit all your values just like before, the Rect Transform also has a menu for setting Pivot and Scaling Centers to predefined places.
This is very important later when looking at responsive User Interfaces. For now just have a look at and be aware that it’s there.
If you select one of your Buttons, you will notice an “Image” Component and a “Button” component in the inspector. The Image Script is relatively straight forward, you can add an Background Image to your Button if you like to. This is especially useful when you have designed your UI in a program like Photoshop beforehand. I haven’t done so, an am also not very fond of the standard UI Sprite, so I set the Source Image to None.
The Button Component serves multiple purposes. For one it handles the visual appearance of the button when you hover over it, select it and so forth. You can define colors and alpha here. As well as the duration it takes to fade between these values.
On the other hand the Button Component handles what actually happens once you click the Button. But to actually have it do something, we of course need a script! So let’s plan out our Scripts!

### User Interface Scripting
So what do we want to achieve?
1. Have Start button that loads our first sketch/scene.
2. Have two buttons to navigate between sketches/scenes.
3. Switch between the Start Screen and the actual Scene Navigation Screen.
4. We want to retain our User Interface, so we don’t have to embed it into every Scene.
5. Have a Quit button to actually leave the application.

#### Scene Management and Building
To be able to properly talk about scripting this, we need to take a little intermezzo and talk about Scene Management and how to actually build or deploy your app.
To actually create a self contained application from your project we need to go through a process called “building”. Building your application is platform dependent and the simplest thing, and the thing we look at right now, is building for the platform you are working on right now. To go to the Build Settings, go “File ---> Build Settings...” or simply press “Ctrl/Cmd + Shift + B”. You will be greeted by this window:
TODO Add Image Build Settings
On the top of the window you will find a list of all the scenes that are currently included in your built. You can drag and more scenes from the project window in here. Take a look at the numbering on the right side. This will be the order in which the scenes will be loaded if you load you scenes by simply increasing the build index, as we will approach to do.
In the bottom left you find your selected platform. If this is currently not set to “Windows, Mac & Linux Standalone”, select that entry and click the “Switch Platform” button. If it is set correctly and you have the scenes selected you want to include you can go ahead an press “Build and Run”. Unity will ask you to select a folder to which you would like to build. If there are no errors in your project Unity will then directly run the project from that folder. But up to now you are not able to switch between scenes. So let’s move on to Scene Management.
 Scene Management is done using the `UnityEngine.SceneManagement` namespace. It allows you to load and unload scenes at runtime. It also has access to all the information about how many scenes were actually staged in the build. We also have different methods of loading our scene. We can either provide the actual name of the scene or put in the index in the Build list. In an App where we want to just go through them one by one this is the more convenient way of loading scenes for us. So let’s look at the script.
{{<highlight c>}}
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using UnityEngine.SceneManagement;
 
public class SketchSwitcher : MonoBehaviour
{
    public void StartSketches(){
        SceneManager.LoadSceneAsync(1);
    }
 
    public void NextSketch()
    {
        int sceneToLoad = SceneManager.GetActiveScene().buildIndex + 1;
        CheckAndLoadScene(sceneToLoad);
    }
 
    public void PreviousSketch(){
        int sceneToLoad = SceneManager.GetActiveScene().buildIndex - 1;
        CheckAndLoadScene(sceneToLoad);
    }
    
    private void CheckAndLoadScene(int sceneToLoad)
    {
        if (CheckIfSceneExists(sceneToLoad))
        {
            LoadMyScene(sceneToLoad);
        }
    }
 
    private void LoadMyScene(int sceneToLoad)
    {
        SceneManager.LoadSceneAsync(sceneToLoad);
    }
 
    bool CheckIfSceneExists(int sceneToLoad){
        if (sceneToLoad <= 0){
            return false;
        }else if(sceneToLoad > SceneManager.sceneCountInBuildSettings -1) {
            return false;
        }else{
            return true;
        }
    }
 
    void QuitApplication(){
        Application.Quit();
    }
}
{{</highlight>}}

We have the Scene Management namespace included and got rid of all the basic Unity methods, because we don’t actually need them. The first method we created will load the first sketch.
The other methods will first check for the current BuildIndex number and the increase and decrease for Next and previously respectively. Before actually calling the load function, we will check if the scene we want to load actually exist to avoid Null Reference Errors.
Now to get our buttons working we need to get our Script somewhere into the scene. You can either add it to our “User Interface” GameObject or add it to the Canvas. It actually doen’t really matter. It just hast to be in the scene.
Next we need to connect these things up. And this is actually a little counter-intuitive:
1. Select the first Button you want to add functionality to.
2. Click the little `+` in the lower right corner of the OnClick() area on the button component.
2. Drag and Drop the GameObject you add your Script to into the empty slot on the OnClick field on the Button Component.
3. Then right next to that field a dropdown menu becomes active. From this dropdown menu select the from the script we wrote the method that should be called when the button is clicked.
4. Repeat this for all the Buttons you want to set up.
TODO Set up some UI Gifs
Another little Gotcha! with this is, that all functions you want to show up in that list, have to actually be public.

If you actually run this now, you will run into trouble. Scene Management by default assumes, that once you load a new scene, you want to get rid of the scene you are currently in. Which makes perfect sense, I guess. Yet this means we will instantly loose our User Interface, when we click the Start Button. Thus we need a way to retain our User Interface. To do this Unity offers us the `DontDestroyOnLoad()` function. Any Object that calls this function will not be destroyed in a loading process. And that’s why we added another GameObject to hold our Canvas and EventSystem. Because we want both of them to survive. Now we can just add a script calling `DontDestroyOnLoad()` to the top GameObject:
{{<highlight c>}}
using UnityEngine;
 
public class DontDestroyOnLoad : MonoBehaviour
{
    void OnEnable(){
        DontDestroyOnLoad(this.gameObject);
    }
}
{{</highlight>}}

No the there is still on problem remaining. If we press the Start Button it stays. And our Navigation Screen is not enabled, if you have it disabled. There is no change at all. Well for small menus there is an easy fix for this. We can simply add more events to the OnClick Event on the Button Component. On the Start Button add two more events to the OnClick List. Then Drag and Drop the StartScreen and the NaveScreen GameObjects from the Hierarchy in the Slots. This time choose the “GameObject ---> Set Active (bool)” from the menu. Then Check the box for the NavScreen and Un-Check the checkbox for the MainMenu Screen.
If you haven’t yet disabled the Screen_NavMenu in your scene, go ahead and do it from the editor.

And now you should have a working User Interface that you can use to show off the sketches you have created so far.


### Project 1 - UI Testing App
### Project 3 - Really bad User Interfaces






