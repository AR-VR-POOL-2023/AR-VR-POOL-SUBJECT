# AR/VR Day 01: Augmented Reality

## Prerequisite

Download the latest LTS version of Unity (2021.3)

Install the two modules Android Build Support via Unity Hub

## Exercise 01 : Scene setup

To build the AR project, we are going to use a package called « AR Foundation ».

To install this package, go to the unity package manager. In the list of offered packages, select « ARFoundation » and install it, as well as «ARCoreXR Plugin» package.

Once both of these packages are installed, go to the « project settings ».
In the XR plug-in Management tab, go to the android sub-tab, and pick «ARCore».

In the Other Settings section:
• Untick the Auto Graphic API checkbox and remove
Vulkan from the list of graphic APIs.  
• In Target Architecture, tick «ARM64».  
• Then, set your Minimum API level to Android 7.0,
and Scripting backend to IL2CPP.  

Back in your Unity scene, right click the « Hierarchy » panel and add two objects:  
• An AR session  
• An AR session Origin.  

> Both of these components are necessary: they will enable your compilation platform to create a session where AR interaction is possible.
>
> This way, the AR session Origin enables you to translate the position of some real objects (like a flat surface) as precise points, with coordinates in > the application, thanks to a tracking system.

Since the AR session already has a camera, you can now delete the base camera from your hierarchy.
Add a new component to your AR session origin object. To do so, select your object, then click «add component» in the inspector.

Add an AR Plane Manager. This ARCore library script will make you capable of detecting flat surfaces through your mobile device’s camera and overlaying a plane on it.
A plane is a flat surface represented by coordinates, dimensions, and bounding points.
You’ll notice that this script awaits several parameters, like the Prefab Plane.

This object will be instantiated in our scene as soon as the plane manager detects a flat surface.

To create that flat surface, add another object to your hierarchy. This time, make it an AR Default Plane.
Pass this new object as a parameter to the AR Plane Manager script.

## Exercise 02: Plane detection

Add a new component to your AR Session Origin: an AR Raycast Manager. This script will enable us to create rays from a point to another, towards a specific direction, on a defined or undefined length.

In our case, we want to create a ray starting from our camera objective, going on for an indeterminate length.
If the ray intercepts an object, it will make it easier for our program to know if the user is pointing the camera at an object or not.

In order to know if our camera ray is intercepting our AR Plane, let’s create a scipt.
In our hierarchy, create a new «AR controller» GameObject.
Add to it a new script type component. The goal of this script is for a cube to spawn when the user touches the screen.

In order to do that, the script will need to know if the camera is pointed to the AR Plane, and if the screen is
being pressed. If it’s the case, we will display a cube:
• Create two variables, a GameObject type one, representing the object to spawn, and a ARRaycastManager one, representing our ray manager.  
• In the Update() function, detect if the user touched the screen.  

> https://docs.unity3d.com/ScriptReference/Input-touchCount.html  

• If the user interacts with the screen, we will ask the RaycastManager if the ray coming from our camera has intersected with our AR Plane.  

> Use the Raycast() function !  

• Then, if RaycastManager finds one or several intersections, then we spawn our GameObject  

Once this script is done, don’t forget to pass an object to spawn as parameter (i.e., a Cube) as well as your RaycastManager using the Inspector tab.
Switch to developer mode on your android smartphone, and enable USB debugging.

Compile your app (Build and Run).

## Exercice 03: Interactive cube 

For this second part, we are going to create an interactive cube. We need to display an information panel when looking directly at a cube, with a simple description on it.

For starters, let’s create a cube in your hierarchy:  
• Add a new GameObject as a child, that we’ll call « InfoPoint ».  
• As a child of that GameObject, add a new quad object. It’s going to be used as our panel. Call it « InfoPanel ».  

Create a new material in your Assets folder. In Unity, materials are components enabling you to add a texture to your objects.
Set up this material to get a color that you enjoy, and add some transparency (in order to do that, don’t forget to set the “Rendering mode” parameter to transparent)

Let’s add some text to our panel:
● Create a « Text – Text Mesh Pro » object as an “InfoPanel”. Accept the « TMP essentials » imports.  
● Using the gizmo around the text, or the Transform parameter, make the text zone smaller, so that it fits our panel.  
● Tick the AutoSize checkbox, and set the min and max parameters respectively to 0 and 1000.  
● Then, slightly pull the text so that it’s not colliding with the panel.  

In order to create our panel’s animation, we need to move the gizmo from our « InfoPoint ».  
Move your infoPoint directly in contact with the top of our cube. We’ll be able to toy with a “Scaling” extension, to display our panel.

## Exercice 04: Hide and seek
