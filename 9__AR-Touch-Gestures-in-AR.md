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

#### Now that we have the Plane, we can finally start

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
using UnityEngine.XR.ARFoundation;
using UnityEngine.XR.ARSubsystems;

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
