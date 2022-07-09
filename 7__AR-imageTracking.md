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
