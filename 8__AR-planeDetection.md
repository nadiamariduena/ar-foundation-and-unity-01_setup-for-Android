### AR [Plane Detection](https://youtu.be/uWWiYfPTUtU) 🥭

<br>
<br>

### Start by creating a new project 🌻

- change the name of the project

- repeat all the steps from ✋ [step 6](./6__AR-foundation.md)

<br>

[<img src="./read-img/create-a-project.gif"/>]()

<br>

- After that go to the **Build Settings > PLayer Stetings** and repeat all the steps from ✋ [step 6](./6__AR-foundation.md)

<br>

### Setting up the scene 🍭

<br>

- Click on **AR Session Origin** (left side) and under the AR Session Origin component (right side), click on **Add component**, once the dropdown opens choose **AR plane manager**

<br>

[<img src="./read-img/plane-manager.gif"/>]()

<br>

### AR plane manager 🍰

> The plane manager creates GameObjects for each detected plane in the environment. A plane is a flat surface represented by a pose, dimensions, and boundary points. The boundary points are convex.

##### Docs: [AR plane manager](https://docs.unity3d.com/Packages/com.unity.xr.arfoundation@4.0/manual/plane-manager.html)

<br>

> You can specify a detection mode, which can be horizontal, vertical, or both. Some platforms require extra work to perform vertical plane detection, so if you only need horizontal planes, you should disable vertical plane detection.

<br>

[<img src="./read-img/ar-plane-manager-detection-mode.png"/>]()

<br>

### Plane Prefab 🍰

> **When a plane is detected, the AR Plane Manager instantiates the Plane Prefab** to represent the plane. The Plane Prefab can stay null, but the plane manager ensures the instantiated GameObject has an ARPlane component on it. The ARPlane component only contains data about the detected plane.

##### read more: [AR plane manager](https://docs.unity3d.com/Packages/com.unity.xr.arfoundation@4.0/manual/plane-manager.html)

<br>

### Create the Plane Prefab 🍰

- After creating the Plane manager, you will see that there is a **Plane prefab** required, at the moment in our project we dont have one. ✋ There are some pre build **prefabs** you can use from the **unity samples** (they look like this [minute: 5:18](https://youtu.be/uWWiYfPTUtU?t=318))

<br>

#### Go to the left side and add the following:

<br>

- Right click **create an empty** object, rename to ARPlne, then go to the right side and **add component**

- add this 3 components: AR Plane , AR PlaneMesh visualizer, MeshCollider ✋

<br>

[<img src="./read-img/ARPlane_ARPlaneMesh_MeshCollider.gif"/>]()

<br>

#### After that we need to add 2 more components in the same place, as we need a way to visualize our place, so that is going to be:

- A **Mesh Filter**

- and a **Mesh renderer**

[<img src="./read-img/ar-default-plane1.png"/>]()

<br>

> When I create the cube to test, you will see that it keeps everything on top of its component

[<img src="./read-img/meshFilter__MeshRenderer.gif"/>]()

<br>

### Line Renderer :sunflower:

<br>

#### Change some settings in the <u>line renderer</u>

- Change the width to: 0.01

<br>

- Change the **Corner Vertices** to 4 and the **End Cap Vertices** also to 4

<br>

- Change the color (whatever you like)

<br>

- Disable the **Use World space**

- in **Lighting** change the **Cast Shadows** from on to **off**, disable the **Receive Shadows**

<br>

- Open the little arrow inside the **Materials > Elements**, once the window open choose the "Default Line" white cube

<br>

[<img src="./read-img/LineRenderer-settings.gif"/>]()

<br>

##### Now that I am done with the line render, add a material.

<br>

### Material :sunflower:

- Right click on the assets, when the menu opens, Create a folder, call it **materials**

<br>

- Click on the materials folder and create a **material** (right click to open the menu)

<br>

click on the material, go to the right side and change the **opaque to transparent**

<br>

- Click on the color and reduce the opacity to 75, As you can see you have the **R,G,B,A**, change only the A from 255 to 75

<br>

[<img src="./read-img/material-before-prefab.gif"/>]()

<br>
<br>

#### 🍭 Now that we are done with the settings, we can make a PREFAB out of all this

- Go to the assets, create a folder and call it **PREFABS**

<br>

- click on the prefab folder, once in, drag the ARPlane from the top, and drop it inside the **prefab folder**

<br>

- Once you do that, click on **AR Session Origin** , at the right side you will see the 2 components: Ar session origin and AR Plane Manager

<br>

[<img src="./read-img/prefab-ready.gif"/>]()

<br>

- DRAG the **ARplane** form the prefab folder, into the **AR Plane Manager** (inside the Plane prefab) , if it doesn't work click on the little arrow of the AR Plane Manager, a window will open, once there choose the **ARPlane**

<br>

<br>

[<img src="./read-img/prefab-ready2.gif"/>]()

<br>
