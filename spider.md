# 🍨

## [Beginners guide to UNITY AR Foundation (ARKit & ARCore) - Build your first AR app from scratch!](https://youtu.be/KqzlGApWPEA)

<br>

- Start by creating a new **3D** project, then once its created we will see that we have the basic set up(we dont have yet the XR "packages"), so at this point we just have the **Main Camera and the Directional Light**

<br>
<br>

### Start by importing the XR packages 🌈

<br>

- Go to **window** > **package manager**

<br>

- Click on the arrow on the top of the window, then once the dropdown unfolds, click on the **Unity registry**, you can either install all the AR packages related, or you can also avoid unfolding the menu and just scroll down to do it one by one. **LOOK FOR** ARCore XR Plugin, and install it, repeat the same steps with the ARFoundation and the ARKit XR Plugin

<br>

- The tutorial was created a year ago so the version he is using are different **(3.1.8)**, right now I will be using the **(4.2.3)**

<br>

> 🔴 I will try this tutorial with this new version to see if it works, if it doesn't work I will try to downgrade few versions.

<br>

- ✋ After installing the packages you will notice the **XR folder** has been creating and is now in your unity dashboard

<br>

- ✋ Delete the default camera, as we will be using the XR main camera

<br>

- ✋ Add the <u>AR Session Origin</u> **(it contains the AR camera)**

<br>

## Now we need an indicator

- This indicator will help us see where do we spawn our **Game object**

<br>

- ✋ Create an **EMPTY Game object**, right click under the **AR Session** (click on the dark space), once you right click on it and the menu unfolds, choose **Create Empty**

<br>

- ✋ Once the empty has been created, change the empty name from GameObject to **PlacementIndicator**

<br>

[<img src="./img-spiderapp/creatingEmpty-changingName.gif"/>]()

<br>
<br>

> 🍨 Now that we have changed the name of the **empty**,

<br>

- ✋ **Right click** on the **empty** to unfold the menu, once the **menu opens** choose **3D Object > Quad**

<br>

[<img src="./img-spiderapp/empty-create3dObject.gif"/>]()

<br>

### Rotate the Quad 🍒

- **Go to the right side** of the window (don't forget to click on the quad, OTHERWISE you will not see the options)

### Scale 🍒

- change the scale to 0.3 on the **x y z axis**

<br>

[<img src="./img-spiderapp/rotating-and-scaling.gif"/>]()

<br>

<br>

## The script

- ✋ Add another **empty** Object and call it **controller**

<br>

- ✋ Then go under the component where you change the name of the empty, and click on **add component**, there type **ARplacement**, you will not find it in the menu but click on **Script** then once it gives you the option of adding it, click on it (check the zoomed version of the image below)

<br>

[<img src="./img-spiderapp/createNewEmpty-callIt-controller-then-create-script.gif"/>]()

<br>

#### Here I created it a second time just for testing 🍰

[<img src="./img-spiderapp/createNewEmpty-callIt-controller-then-create-script2.gif"/>]()

<br>

#### ✋ Now that we have the SCRIPT that will help us to put all the logic, lets check if we have all the _complementary_ scripts we will need in our <u>_AR Session Origin_</u> ✋

<br>

- 🔴 add the **AR Plane and the AR Raycast manager**

<br>

[<img src="./img-spiderapp/Add-plane-and-raycast-manager.gif"/>]()

<br>

#### Start working on the script 🍉 🥭

- This is the basic layout of the script

```javascript
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class ARplacement : MonoBehaviour
{
    // Start is called before the first frame update
    void Start()
    {

    }

    // Update is called once per frame
    void Update()
    {

    }
}

```

<br>
<br>

#### Read the steps

```javascript
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
// 5
using UnityEngine.XR.ARFoundation;

public class ARplacement : MonoBehaviour
{

// 1
public GameObject arObjectToSpawn;
// 2
public GameObject placementIndicator;
// 10 related to the method in step 9
private GameObject spawnedObject;

//
// 3
private Pose PlacementPose;
// 4
private ARRaycastManager aRRaycastManager;
// 6
private bool placementPoseIsValid = false;


    //
    //
    // Start is called before the first frame update
    void Start()
    {
        // 7
        aRRaycastManager = FindObjectOfType<ARRaycastManager>();
    }

    // Need to update placement indicator (when moving the phone), (then keep track)of the placement "pose" (position) while moving the phone and spawn the AR object. Now in step 8 we will make a function for each one of these
    void Update()
    {
        // 8 make a function for each one
        UpdatePLacementPose();
        UpdatePlacementIndicator();
    }
    // 9 create the methods linked to the functions in step 8
    //
    //  METHOD :     UpdatePlacementIndicator();
    //
    void UpdatePlacementIndicator()
    {
        //11 after creating the private variable in step 10, create the conditional handling the
        //movement *TRANSFORM:  position, rotation:
        if(spawnedObject == null && placementPoseIsValid)
        {
            // 12
            placementIndicator.SetActive(true);
            // 13
            placementIndicator.transform.SetPositionAndRotation(PlacementPose.position, PlacementPose.rotation)
        }else{
            // 14
            placementIndicator.SetActive(false);
        }
    }
    //15  METHOD :    UpdatePLacementPose();
        void UpdatePLacementPose()
        {
            // 16
            // here we will need to give the position of the placement indicator in the screen center, using the current camera, which is the  AR camera
            //  Vector3(0.5f, 0.5f), makes reference to the 0.5 X and 0.5 Y, which is exactly at the center of the screen
            var screenCenter = Camera.current.ViewportToScreenPoint(new Vector3(0.5f, 0.5f));
            // 17
            // then lets get all the HITS and create a List with the "ARRaycastHit" on it. (in other words, inside the list you will add the ARRaycastHit component)
            var hits = new List<ARRaycastHit>();
            // 18
            // Then using the  ARRaycastManager, Raycast, screenCenter, and the hits, we calculated on the trackable planes
            aRRaycastManager.Raycast(screenCenter, hits, TrackableType.Planes);
            //    so here above we have the aRRaycastManager that we have defined on the top (where the variables are) and then this one is going to use the "raycast" method which then give us a touch position, then it takes the "hits" from our static list in step 17,

            //
            // 19
            // Add a condition, that if the hits dot count is greater than 0, then
            // change the boolean accordingly
            //
            // if the Input.TouchCount is greater than 0 , then we want to get the touchPosition and then return  true, because we are returning a boolean, and if there is nothing (if there is not touchCount) then the touch position stays as default, so if there is not touchCount we are returning false
        touchPosition = Input.GetTouch(index 0).position;
            placementPoseIsValid = hits.Count > 0;
            if(placementPoseIsValid)
            {
                // 20
                // and further check if the placement pose is valid, then get the very first hit and store it in the placement pose
                PlacementPose = hits[0].pose;
                //
//  check step 11            then we have to figure out if there is a "hit" object already, if there is none, then we want to instantiate it (create one) and if there is an object already then we want to basically move it around, it will totally depends on the use case, basically what we want to build in this demo which is also from the ARFoundation samples, is that if there is an object already, then we just wanted to have this one cube to move around, but you can use anything, you can also limit it to 5 objects, here it will totally depends on your demo and whatever you want to build
                //
            }
        }
        // 21
        // to place the ar object, simply store it in the spawn  by using "instantiate", the instantiate stuff inside the paranthesis is calculated in step
        void ARPlaceObject()
        {
            spawnedObject = Instantiate(arObjectToSpawn, PlacementPose.position, PlacementPose.rotation);
        }
        // 22 after this, go back to the update function, and call the ARPlaceObject() function
}

```

<br>

> 🔴 Go to unity and check for errors, if it tells you there is "," or a ";", click twice in the error on the unity console, it will open VS exactly where the error is, and add what its asking. If you get an error like **TrackableType** dont exist, add this **using UnityEngine.XR.ARSubsystems;** on the top of the file where all the libraries are required, he didnt add it on the tutorial because I think the version he is using already has it.

<br>
<br>

#### After step 22:, go back to the update function, and call the ARPlaceObject() function

```javascript
// 23  calling the method ARPlaceObject in the update function (which is here), when there is nothing in the spawnedObject, by nothing i meant not touch
if(spawnedObject == null && placementPoseIsValid && Input.touchCount > 0 && Input.GetTouch(0).phase == TouchPhase.Began){
    //24 calling the function in step 21
    ARPlaceObject();
}


        //
        //
        // 8 make a function for each one
        UpdatePLacementPose();
        UpdatePlacementIndicator();
    }
    // 9 create the methods linked to the functions in step 8
    //
```

<br>
<br>

#### SO this is what we have

```javascript
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
// 5

using UnityEngine.XR.ARFoundation;
using UnityEngine.XR.ARSubsystems;

public class ARplacement : MonoBehaviour
{

// 1
public GameObject arObjectToSpawn;
// 2
public GameObject placementIndicator;
// 10 related to the method in step 9
private GameObject spawnedObject;

//
// 3
private Pose PlacementPose;
// 4
private ARRaycastManager aRRaycastManager;
// 6
private bool placementPoseIsValid = false;


    //
    //
    // Start is called before the first frame update
    void Start()
    {
        // 7
        aRRaycastManager = FindObjectOfType<ARRaycastManager>();
    }

    // Need to update placement indicator (when moving the phone), (then keep track)of the placement "pose" (position) while moving the phone and spawn the AR object. Now in step 8 we will make a function for each one of these
    void Update()
    {


// 23  calling the method ARPlaceObject in the update function (which is here), when there is nothing in the spawnedObject, by nothing i meant not touch
if(spawnedObject == null && placementPoseIsValid && Input.touchCount > 0 && Input.GetTouch(0).phase == TouchPhase.Began){
    //24 calling the function in step 21
    ARPlaceObject();
}


        //
        //
        // 8 make a function for each one
        UpdatePLacementPose();
        UpdatePlacementIndicator();
    }
    // 9 create the methods linked to the functions in step 8
    //
    //  METHOD :     UpdatePlacementIndicator();
    //
    void UpdatePlacementIndicator()
    {
        //11 after creating the private variable in step 10, create the conditional handling the
        //movement *TRANSFORM:  position, rotation:
        if(spawnedObject == null && placementPoseIsValid)
        {
            // 12
            placementIndicator.SetActive(true);
            // 13
            placementIndicator.transform.SetPositionAndRotation(PlacementPose.position, PlacementPose.rotation);
        }else{
            // 14
            placementIndicator.SetActive(false);
        }
    }
    //15  METHOD :    UpdatePLacementPose();
        void UpdatePLacementPose()
        {
            // 16
            // here we will need to give the position of the placement indicator in the screen center, using the current camera, which is the  AR camera
            //  Vector3(0.5f, 0.5f), makes reference to the 0.5 X and 0.5 Y, which is exactly at the center of the screen
            var screenCenter = Camera.current.ViewportToScreenPoint(new Vector3(0.5f, 0.5f));
            // 17
            // then lets get all the HITS and create a List with the "ARRaycastHit" on it. (in other words, inside the list you will add the ARRaycastHit component)
            var hits = new List<ARRaycastHit>();
            // 18
            // Then using the  ARRaycastManager, Raycast, screenCenter, and the hits, we calculated on the trackable planes
            aRRaycastManager.Raycast(screenCenter, hits, TrackableType.Planes);
            //    so here above we have the aRRaycastManager that we have defined on the top (where the variables are) and then this one is going to use the "raycast" method which then give us a touch position, then it takes the "hits" from our static list in step 17,

            //
            // 19
            // Add a condition, that if the hits dot count is greater than 0, then
            // change the boolean accordingly
            //
            // if the Input.TouchCount is greater than 0 , then we want to get the touchPosition and then return  true, because we are returning a boolean, and if there is nothing (if there is not touchCount) then the touch position stays as default, so if there is not touchCount we are returning false

            placementPoseIsValid = hits.Count > 0;
            if(placementPoseIsValid)
            {
                // 20
                // and further check if the placement pose is valid, then get the very first hit and store it in the placement pose
                PlacementPose = hits[0].pose;
                //
//  check step 11  and 23          then we have to figure out if there is a "hit" object already, if there is none, then we want to instantiate it (create one) and if there is an object already then we want to basically move it around, it will totally depends on the use case, basically what we want to build in this demo which is also from the ARFoundation samples, is that if there is an object already, then we just wanted to have this one cube to move around, but you can use anything, you can also limit it to 5 objects, here it will totally depends on your demo and whatever you want to build
                //
            }
        }
        // 21
        // to place the ar object, simply store it in the spawn  by using "instantiate", the instantiate stuff inside the paranthesis is calculated in step
        void ARPlaceObject()
        {
            spawnedObject = Instantiate(arObjectToSpawn, PlacementPose.position, PlacementPose.rotation);
        }
        // 22 after this, go back to the update function, and call the ARPlaceObject() function
}

```

<br>
<br>

#### Go back to unity ☕

> At this point with the code above you shouldn't have any error

<br>

- Go back to unity and put the script file inside the script folder

- ✋ **CREATE** and folder and call it **scripts** (right click inside the dashboard of your assets)

<br>

[<img src="./img-spiderapp/placementindicator.gif"/>]()

<br>
<br>

### Once you add the scripts inside the Scripts folder 🍒

- ✋ Click on the **Controller**, you will notice that now we have 2 empty fields under **AR object To Spawn** and **Placement Indicator**

<br>

- ✋ Grab the **Placement indicator** and drop it inside the corresponding field

<br>

[<img src="./img-spiderapp/placementindicator.gif"/>]()

<br>
<br>

### Add a model from the assets Store 👾

<br>

- ✋ Go to the store and choose a model, I will be using an **fbx** animated spider

<br>

- Once you have your model, go to your assets in the browser and click open in Unity, (if you are already connected in your unity), go to the **window > package manager** click on the top bar dropdown and choose assets, there you will see the assets, click on the one you want and download it, **once it s ready, click on import** (it will open another window, where you will chose what you want to import from the model) click again import it, now go back to your **unity assets** and check the model.

<br>

#### choose model 🍰

[<img src="./img-spiderapp/chooseModel-from-unityStore1.gif"/>]()

<br>

#### Download model 🧁

[<img src="./img-spiderapp/downloadModel-from-unityStore1.gif"/>]()

<br>
<br>

## Lets see what the model contains 🍉

- inside of the model you will notice a couple of animations

<br>

[<img src="./img-spiderapp/model-animations-fbx.gif"/>]()

<br>

#### Add an icon to PlacementIndicator

<br>

- go to [flaticon.com](https://www.flaticon.com/)

- Choose a **target** icon, but before downloading it to your unity, create 2 new folders in your assets

<br>

- ✋ CReate 2 new folders, a **Textures** and **Materials**, save the target icon inside the Textures folder(go to your unity project folder inside your comp, look for the one you are working and save it in the Textures)

<br>

- ✋