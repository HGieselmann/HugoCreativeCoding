Disclaimer: This chapter is written based on Unity 2019.2 and ARFoundation Package Version 2.0.2. I can only properly show the setup for Android Phones as well, as I do not have an iOS development environment.

### Augmented Reality Definition
### Designing for Augemented Reality
Augmented Reality is one of the most interesting fields in design right now. In contrast to print or webdesign many of the precieved rules are not yet written. So you can still come up with radically new ways for designing in augmented reality and grab the attention of your users.
On the other hand augmented reality already advanced enough for it to have some technological base that you can rely on. Apple came up with it’s ARKit framework for more recent iPhones and Googles Android System implements it’s ARCore Library to create Augmented Reality experiences. Adding on top of that are more and more devices like Microsoft’s Hololens bring these experiences directly into your field of vision.
Better yet, the folks at Unity provide a Package called “ARFoundation” which aims to integrate ARCore, ARKit and many other XR Frameworks into one. Thus we as developers only have to deal with and ARFoundation and Unity will handle the implementation differences between iOS, Android an the other devices.
As you can see Augmented Reality is a great place to experiment, work and design in right now.

### Setting up AR Foundation for Android
To develop AR applications in Unity you first and foremost need an ARCore compatible device. Sadly that includes only the more recent flagship and upper middleclass phones. Check the List of compatible devices here:
Link to compatible device list
Next you need to make sure your devices (PC and Phone)are properly configured for android development. To check what to follow the guide Unity created:
https://docs.unity3d.com/Manual/android-sdksetup.html
So once you are ready to start, create a new “3D” Project and open the Package Manager from Windows > PackageManager

