## New Test 🍨

#### I am actually testing a new way of setting things up, I will be documenting things at the end of it

```javascript
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class ARPlacement : MonoBehaviour
{

/*
✋
What i learned today:
 Since i am new with unity and C#, i discovered that this
 variable in this script here below "GameObject" is linked with the "empty" i create in unity, at the left side of the window (under the sessions"), this empty appears as GameObject when you create, then after it s created you can change the name to whatever you want, in this case i changed it to placementIndicator


*/

public GameObject arObjectToSpawn;
public GameObject placementIndicator; // check the LOWERCASE in the P of placement, as in unity we have it as PlacementIndicator and not placementIndicator
//
private GameObject spawnedObject;

private Pose PlacementPose;

/*
✋
this "ARRaycastManager" too corresponds to something I have in Unity, its actually the component I create under the session origin (right side of the window)


*/
private ARRaycastManager aRRaycastManager;
private bool placementPoseIsValid = false;

    // Start is called before the first frame update
    void Start()
    {
        aRRaycastManager = FindObjectOfType<ARRaycastManager>();
    }

    // Update is called once per frame
    void Update()
    // ✋ a create the methods, to use this methods create this variable on top of the file: private GameObject spawnedObject; 🍭
    {
        UpdatePlacementPose();
        UpdatePlacementIndicator();
    }
    //
    //
    // ✋ b fill the methods
    void UpdatePlacementIndicator()
    {
        if(spawnedObject == null && placementPoseIsValid)
        {
            placementIndicator.SetActive(true);
            placementIndicator.transform.SetPositionAndRotation(PlacementPose.position, PlacementPose.rotation);

        }
        else
        {
            placementIndicator.SetActive(false)
        }
    }
    //
    //
    //
    void UpdatePlacementPose()
    {
        var screenCenter = Camera.current.ViewportToScreenPoint(new Vector3(0.5f, 0.5f));

    }
}

```

got to the packet manager and install this:

don't go to the AR to install all directly, instead scroll down and only install the:

ARFoundation
ARCore XR Plugin

ARKit XR Plugin

close the window and go to the scene, then remove the camera and add the origin session + the session form the XR

Now that we have the two above, we need an indicator so that we can see where do we spawn our game objects

create an _empty_ game object, at the right side of the window change the name to PlacementIndicator, now right click on the PlacementIndicator, choose create 3d, then choose the 3d shape: quad

change the Rotation of the X axis to 90, change the scale of the 3 axis to 0.3

NOW we need to add a script SPAWN

click on the left side of the window ( where the session is)

- add another empty, then change the "empty" name to GameObject
