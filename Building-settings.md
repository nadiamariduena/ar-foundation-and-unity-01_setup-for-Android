## Export settings 🍰

#### This is the basic you need to build the scene, but not all the projects are the same, so you will need different setting depending on what you are working on.

<br>

---

<br>
<br>
<br>

### Android 👾

<br>

- If you haven't done it already, switch to the **android** platform (**File > Build settings** )

<br>

> ✋ then click on the **Player settings** , once it opens this new window , go to **Player**, then check the arrow with the **Other settings**, once there:

<br>

- At the top of the window, choose a name, by default you have (Default Company) , but you can change that to whatever you want, for this project i will add **DefaultCompanySpider**

<br>

- change the **Color Space** from Gamma to **Linear**

<br>

- check the **AutoGraphics** , you will have to options there for the graphics API: OpenGLE3 and Vulkan, delete the vulkan by clicking in the minus - (at the right side of the window)

<br>

- Now scroll down in the same window, go to the **Minimum API Level**, choose Android 7.0 Nougat (API level 24)

<br>

[<img src="./img-spiderapp/basic-building-setup.gif">]()

<br>
<br>

#### Close the window and go back to the scene 🌈

<br>

- go to **window > General > Game** once it creates the tab, go to the aspect ratio and choose **1920 x 1080**

<br>

[<img src="./img-spiderapp/aspectRatio.gif">]()

<br>

#### Now that you have the settings above, Go back to the payer settings

<br>

- ✋ **File > Build settings**
  <br>

> ✋ then click on the **Player settings** , once it opens the window , go to **Player**, then check the arrow with the **Resolution and Presentation** tab, once there:

<br>

- Go to the **Default Orientation** , choose **Portrait**, close the window.

<br>

<br>

[<img src="./img-spiderapp/aspectRatio2.gif">]()

<br>

> ##### Don't forget to add the scene, like you see at the end of the gif above

<br>
<br>

#### 🔴 ARCore Plugin

<br>

> ✋ A last thing... check the the **XR Plug-in Management** so that you don't have the black screen issue, when testing it with your phone.

<br>

- (**File > Build settings** )

<br>

> ✋ then click on the **Player settings** , click on the **XR Plug-in Management** then **check** the **ARCore** thats all (in some versions you will have to click on install then you have the option to check on the arcore)

<br>

[<img src="./img-spiderapp/arcore-plugin-building-settings-avoid-blackscreen.gif">]()

<br>
