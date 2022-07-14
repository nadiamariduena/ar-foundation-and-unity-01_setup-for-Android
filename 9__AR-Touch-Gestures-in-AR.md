## [Placing and Manipulating Objects in AR](https://youtu.be/xguiSueY1Lw)

##### credits article: [Learn unity.com](https://learn.unity.com/tutorial/placing-and-manipulating-objects-in-ar#)

<br>

[<img src="./read-img/placing-and-manipulating-objects-in-AR.jpg"/>]()

<br>
<br>

---

<br>
<br>

# 🌞

#### Start by setting up the basics

- 1. Follow this steps: [6\_\_AR-foundation](https://github.com/nadiamariduena/ar-foundation-and-unity-01_setup-for-Android/blob/master/6__AR-foundation.md)

<br>

[<img src="./read-img/ar-basic-setup.gif"/>](https://github.com/nadiamariduena/ar-foundation-and-unity-01_setup-for-Android/blob/master/6__AR-foundation.md)

<br>
<br>

- 2. **Now set up the Plane** settings, follow the steps here: [/8\_\_AR-planeDetection.md](https://github.com/nadiamariduena/ar-foundation-and-unity-01_setup-for-Android/blob/master/8__AR-planeDetection.md)

[<img src="./read-img/material-before-prefab.gif"/>](https://github.com/nadiamariduena/ar-foundation-and-unity-01_setup-for-Android/blob/master/8__AR-planeDetection.md)

<br>
<br>

## 🍰

## Now that we have the Plane, we can finally start

<br>

#### 🔴 DONT WORRY about the script, after I am done with the AR basic course, I will continue with [Learn C# for Unity](https://xrbootcamp.com/pre-coding-course/)

<br>

- Create a new folder (right click in the assets, once the menu opens, click on **create > folder**) , name the folder **Scripts**

<br>

- Inside the **script** folder , right click to open the menu again, choose **create > script**, name the script "AR_taptoPlane"

<br>

#### Once you have the script, click twice on the file to open the VS editor

<br>

- Once the editor opens, start by importing some libraries

```javascript
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using UnityEngine.XR.ARFoundation;  ✋
using UnityEngine.XR.ARSubsystems;  ✋

public class NewBehaviourScript : MonoBehaviour
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

[<img src="./read-img/scriptPlaceDetection.gif"/>]()

<br>
<br>

#### Add the variables

```javascript
   //2 now create some variables
//    first we will start with a pubic variable:    gameObjectToInstantiate
public GameObject gameObjectToInstantiate;
//
// 3 then private variables: spawnedObject
private GameObject spawnedObject;
// 4
private ARRaycastManager _arRaycastManager;
//  5
private Vector2 touchPosition; //the position will be use when we
// will tap on the screen to then detect where we have to shoot our
// raycast and where to place out object
//
// 6 the last thing we need is a reference of our raycast hits, so
// here below we will create a static list of our "raycast hits"  List<ARRaycastHits>
// call it "hits"
//
static List<ARRaycastHits> hits = new  List<ARRaycastHits>();

```

<br>

#### If you know already that there are some components which are required for your component to work,

- you can use the required component field on top of the class so basically like this (look at the top of the class)

```javascript
// 1 import the 2 libraries below( UnityEngine.XR.ARFoundation, UnityEngine.XR.ARSubsystems)
using UnityEngine.XR.ARFoundation;
using UnityEngine.XR.ARSubsystems;



//7  ✋
[RequiredComponent(typeOf(ARRaycastManager ))]
//
//
public class ARTapToPlaceObject : MonoBehaviour{}
```

<br>

> At this point if we added our **ARTapToPlaceObject** from above, on to any game **object**, it will automatically add this one as well **<u>ARRaycastManager</u>** , then we can just use it free without just checking if we have the object because we know we have this component **<u>ARRaycastManager</u>** as well.

<br>
<br>

#### We can now get rid of our Start() function, and instead an awake() function

```javascript
//
//
// 👍 delete the below
void Start();
{
}
```

<br>
<br>

#### Add this instead

```javascript
//
   private void Awake()
   {
    // ✋   Here we are going to reference our raycasting
   }
```

<br>

#### add this inside the above function

- Here we are going to reference our raycasting

```javascript


    //    ✋
       _arRaycastManager = GetComponent<ARRaycastManager>();


```

<br>

#### we are free to use the line above, because we added this component on the top of the class

```javascript
//7  ✋
[RequiredComponent(typeOf(ARRaycastManager))];
```

<br>
<br>

#### 🔴 DONT WORRY about the script, after I am done with the AR basic course, I will continue with [Learn C# for Unity](https://xrbootcamp.com/pre-coding-course/)

<br>
<br>

#### Now we will handle the conditional for the touch events

<br>

- for this basic input we are going to use the **get touch** method

#### we will be using vector2: so [What is a Vector2 and Vector3 in Unity?](https://stackoverflow.com/questions/54477121/what-is-a-vector2-and-vector3-in-unity)

> It is representation of **2D** vectors and points, used to represent 2D **positions**, only two axis **x&y**

>

<br>
<br>

### Create the method

```javascript
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
// 1 import the 2 libraries below( UnityEngine.XR.ARFoundation, UnityEngine.XR.ARSubsystems)
using UnityEngine.XR.ARFoundation;
using UnityEngine.XR.ARSubsystems;



//7
[RequiredComponent(typeOf(ARRaycastManager ))]
//
//
public class ARTapToPlaceObject : MonoBehaviour
{
   //2 now create some variables
//    first we will start with a pubic variable:    gameObjectToInstantiate
public GameObject gameObjectToInstantiate;
//
// 3 then private variables: spawnedObject
private GameObject spawnedObject;
// 4
private ARRaycastManager _arRaycastManager;
//  5
private Vector2 touchPosition; //the position will be use when we
// will tap on the screen to then detect where we have to shoot our
// raycast and where to place out object
//
// 6 the last thing we need is a reference of our raycast hits, so
// here below we will create a static list of our "raycast hits"  List<ARRaycastHits>
// call it "hits"
//
static List<ARRaycastHits> hits = new  List<ARRaycastHits>();

//



//
//
// 8
   private void Awake()
   {
       _arRaycastManager = GetComponent<ARRaycastManager>();
   }
//
// bool / boolean
// 9
bool TryGetTouchPosition(out Vector2 touchPosition)
{
    // 10
    if (Input.touchCount > 0)
    {
        // if the Inuut.TouchCount is greater than 0 , then we want to get the touchPosition and then return  true, because we are returning a bool, and if there is nothing (if there is not touchCount) then the touch position stays as default, so if there is not touchCount we are returning false
        touchPosition = Input.GetTouch(index 0).position;
        return true;

    }
    //11 here we tell it that we will want the touchPosition to be default
    touchPosition = default;
    return false;
}
// the last thing we will do is to shoot the array in the update method
//
    //12 Update is called once per frame
    void Update()
    {
        // if this one below is false (means that we are not detecting any touch)then we want to return it
        // 13
      if(!TryGetTouchPosition(out Vector2 touchPosition))
      return;
    //
    // 14 ** RAYCAST **
    }
}

```

<br>
<br>

> In C, **Boolean/bool** is a data type that contains two types of values, i.e., 0 and 1. Basically, the bool type value represents two types of behavior, either true or false. Here, '0' represents false value, while '1' represents true value. In C Boolean, '0' is stored as 0, and another integer is stored as 1.

[read more here / C Boolean](https://www.javatpoint.com/c-boolean)

<br>
<br>

# RAYCAST 🍰

<br>

- ✋ When you use raycasting to perform object placement, you can both place an object on a plane, as well as on a feature point or any other trackable. Note that just placing the object in the Unity scene at the intersection point doesn’t anchor the object to the real world (yet!). This means that over time, its perceived position might slightly change, as it’s not attached to the physical object but instead placed in a virtual static coordinate system.

#### Read More: [Raycast & Anchor: Placing AR Foundation Holograms (Part 3)](https://www.andreasjakl.com/raycast-anchor-placing-ar-foundation-holograms-part-3/)

<br>
<br>

#### ✋ So here below we have the _\_arRaycastManager_ that we have defined on the top

```javascript
//
private ARRaycastManager _arRaycastManager;

```

##### And then this one is going to use the raycast method which then give us a touch position, then it takes the "hits" from our static list on the top:

<br>

```javascript

static List<ARRaycastHits> hits = new  List<ARRaycastHits>();
```

<br>

### TrackableType 🍪

##### In general, a trackable in AR Foundation is anything that can be detected and tracked in the real world. This starts with basics like anchors, point clouds and planes. More advanced tracking even allows environmental probes for realistic reflection cube maps, face tracking, or even information about other participants in a collaborative AR session.

#### Read More: [andreasjakl.com / Trackables)](https://www.andreasjakl.com/category/android/)

<br>

[<img src="./read-img/trackables.png "/>]()

<br>

<br>

```javascript
//14 ** RAYCAST **   Now we want to shoot the raycast
// so here below we have the _arRaycastManager that we have defined on the top and then this one is going to use the raycast method which then give us a touch position, then it takes the "hits" from our static list on the top,
if (
  _arRaycastManager.Raycast(
    touchPosition,
    hits,
    TrackableType.PlaneWithinPolygon
  )
) {
  // checkout the trackable type:  https://docs.unity3d.com/2019.2/Documentation/ScriptReference/Experimental.XR.TrackableType.html
}
```
