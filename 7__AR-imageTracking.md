### AR Image Tracking 🍭

<br>

- Once you have the setup from [step 6 ](./6__AR-foundation.md)

<br>

- You can proceed to add a component, this component will handle the image.

<br>

- **TO START**, click on the **AR Session Origin** , once you click on that go to the right side of the window, there click on **add component**, then click on **Ar tracked image Manager** (if you dont find it in the menu, type it)

<br>

[<img src="./read-img/Ar_tracked_image_Manager.gif"/>]()

<br>

[<img src="./read-img/Ar_tracked_image_Manager2.gif"/>]()

<br>

#### For this component, we will need an XR reference

- go to your project, right click to open the menu

<br>

- create > XR > Reference image library

<br>

[<img src="./read-img/Ar_tracked_image_Manager3.gif"/>]()

<br>

[<img src="./read-img/Ar_tracked_image_Manager3.gif"/>]()

<br>
<br>

#### Drag and drop the image to the workspace, then take the image from the workspace and drag it to the component on top (there is a little icon where the image should be)

[<img src="./read-img/Ar_tracked_image_Manager5.gif"/>]()

<br>

#### Specify the size of the image 🌞

<br>

- Here you will specify the size of the image in **meters** , so add something like 30 cm (0.3)

<br>

- **Keep Texture at Runtime** , if you enable this it means that the texture will be available when you press **play**, otherwise the texture will not be on the **player**

<br>

> SO when you are on your phone, you can still exit the picture, but this is going to blow up your phone and the size of your application if you have a **bunch of images stored there**, so you should only keep it if you really need it ( 🔴 not sure of this advise, but with time I will be returning here to explain it better)

<br>

- 🌵 Add other images and give the images names

<br>

[<img src="./read-img/image1_library.gif"/>]()

<br>

#### Now I need to reference the image I just created 🍭

- Drag and drop the reference into the tracked image component, once you do that its going to be detected, but I will need to write a little script

<br>

[<img src="./read-img/image1_referecne1.gif"/>]()

<br>

## Create the Script 🌻

- Once you create the script file, double click on it to open the **visual studio code** , if it doesn't work its because you don't have it yet, so follow this steps to install it: [install VS](./4__integrate-VS-toUnity.md)

<br>

[<img src="./read-img/image1_reference-script.gif"/>]()

<br>
<br>

#### The first thing we are going to do is:

- **add a reference** of our **reference image manager** AR

<br>

- Start by adding this

```javascript
using UnityEngine.XR;
using UnityEngine.XR.ARFoundation;
```

<br>

#### Then add the following functions

> 🔴 If you are new like me in C#, dont worry! I think if you have a bit of experience it will be fine

```javascript
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
// 1
using UnityEngine.XR;
using UnityEngine.XR.ARFoundation;


public class ImageRecognitionExample : MonoBehaviour
{
    // 2
     private ARTrackedImageManager _arTrackedImageManager;

//
// 3
private void Awake()
{
    // 4 this makes reference to the component in unity that contains the reference we dragged and drop (the link to be exact)
    _arTrackedImageManager = FindObjectOfType<ARTrackedImageManager>();
   ;
    //
}
// 5 subscribe when enabled (+)
public void OnEnable()
{
    // here we want to subscribe to the image condition event
   _arTrackedImageManager.trackedImagesChanged += OnImageChanged;
}
//
// 6 unsubscribe when disabled (-)
public void OnDisabled()
{
    // here we want to subscribe to the image condition event
   _arTrackedImageManager.trackedImagesChanged -= OnImageChanged;
}
//
// 7 now write the method (the method is related to the 2 lines of code that we have above) "OnImageChanged"

public void OnImageChanged(ARTrackedImagesChangedEventArgs args)
{
    //8 here we will iterate through the images
 foreach (var trackedImage in args.added)
 {
     Debug.Log(trackedImage.name); //like a console log
 }
}


}

```
