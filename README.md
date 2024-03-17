# UnityQuest2020Template

This template is a starting point for Unity Games on the Meta Quest headset. Feel free to copy the scenes or the game objects, or to build directly off of the scenes. 

This project is made with the following versions in mind:

- Meta Quest 2 Headset
- Unity v2020.3.48
- Oculus Integration Package v50.0

and contains the following features:

- [Camera/controller tracking](#ovr-camera-rig)
- [Grabbing objects](#grabbing-objects)
- [Linear movement](#linear-movement)
- [Teleportation movement](#teleportation-movement)
- [UI raycast interactions](#ui-raycast-interactions)

If this is your first time building a Unity app for the Quest 2 headset, I recommend reading the [**FirstSetup.md** document here](./FirstSetup.md).

In any case, I recommend reading the document's [*using the template* section here](./FirstSetup.md#setting-up-a-new-application-with-the-template).
> Remember to change the Company and Product name in **Edit > Project Settings... > Player**.
>
> The package name should be unique to your project (**Edit > Project Settings... > Player > Other Settings > *Package Name***).

## Scenes

This template has 3 scenes:
- **BaseScene** - this scene has the bare minimum components for VR:
  - *OVR Camera Rig* for VR tracking.
  - Controller models to show where the player's hands are.
  - A plane and text box to look at.
- **WalkingMovement** - this scene demonstrates how to move around, grab items, and interact with UI with the controllers.
  - *OVRPlayerController* - contains the *OVRCameraRig* and movement scripts.
  - *Grabbable Objects* - contains objects setup for picking up (see [grabbing objects](#grabbing-objects)).
  - *Interactive Canvas* - contains the **OVR Raycaster** script and a button to click.
  - *UIHelpers* - contains the laser pointer and event system for clicking on the UI.
  - *SceneManager* - contains a custom script to help with switching scenes.
  - *Environment* - contains the static environment.
  - *Instructions Canvas* - contains non-interactable text.
- **TeleportMovement** - scene is similar to **WalkingMovement**, but with teleport contols instead of linear movement.
  - *PlayerController* - contains the basic movement information.
    - *OVRCameraRig* - camera rig for VR.
    - *LocomotionController* - handles the teleport movement controls and behavior.
  - *Other Objects* - the other objects are the same as the ones listed in **WalkingMovement**.

## Feature Breakdown

This section explains the different features in this template, a brief description of how they work, and how they can be customized.

All of these features could be implemented from scratch for complete control over the behavior, or used as is.
This template just provides the implementations from Meta's Sample Framework to act as a starting point.

### OVR Camera Rig
The *OVRCameraRig* prefab is necessary for any VR app for the Quest 2. This should replace the main camera. You can access the position of the player's controllers using the anchor objects in the Camera Rig's hierarchy.
> This prefab can be found in `Oculus/VR/Prefabs/`.

#### Options
- *Tracking Origin Type* - changes the relationship between the headset's height (in real life) and the camera's height (in game).
  - **Eye Level** - tracking starts at eye level, so the game starts with the in-game cameras exactly where they are in the scene.
    > This means that if you place the camera on the floor of the scene, the player will start with their camera on the floor, even if they are standing up. This can cause the player to feel like they are inside of the ground, or maybe floating above the ground.
  - **Floor Level** - tracking starts from the floor, so the in-game camera will be moved up based on how tall the player (in real life) is from the ground.
    > This means that if you place the camera on the floor of the scene, the player will feel like the ground levels match. If the player moves down to touch the ground, the real-world ground should match the in-game ground.

### Grabbing Objects

To grab objects, use the bottom triggers of the controller! The controllers must have the **OVR Grabber** script, and the objects must have the **OVR Grabbable** script, along with a **Rigidbody** and a **Collider**.

1. Add the *CustomHandLeft* and *CustomHandRight* prefabs to the *OVRCameraRig*.
   > These prefabs are in `Oculus/SampleFramework/Core/CustomHands/`.
   >
   > In addition to having the **OVR Grabber** script, these prefabs have hand models that are animated to match the controller's state.
2. Enable the *Parent Held Object* setting in the inspector for the **OVR Grabber** script in both of the hands.
   > This option makes it so when you grab items, they do not interact with the player's physical colliders. If this option is not enabled, you may run into unwanted physics interactions.
3. Create objects to grab.
4. For these objects, ensure they have the following:
   - **Collider**
   - **Rigidbody**
   - **OVR Grabbable** script
      > This can be found in `Oculus/VR/Scripts/Util/`.
      >
      > The easiest way to add this script is to click *Add Component* and search for `OVRGrabbable`.

#### Options
Feel free to experiment with different settings.

You may want to implement more complex interactions with objects, such as pressing a button when you are holding the object. To do this, write a custom script and access the **OVR Grabber** script.

```
OVRGrabbable grabScript = GetComponent<OVRGrabbable>();

if (grabScript.isGrabbed && OVRInput.Get(OVRInput.Button.PrimaryIndexTrigger)) {
    // Do something
    // Note: this happens when the primary index trigger is pressed, even if the object is grabbed by the secondary hand.
}
```


### Linear Movement

In the *WalkingMovement* scene, the *OVRPlayerController* prefab is used to handle player movement. It enables linear movement and snap rotation, along with many options. Use the left thumbstick to move around. Use the right thumbstick to rotate the camera.

1. Add the *OVRPlayerController* prefab to the scene, which comes with the *OVRCameraRig*.
   > This prefab is in `Oculus/VR/Prefabs/`.

#### Options
Customize how the player interacts with the world using the options in the **Character Controller** and **OVR Player Controller** scripts.

### Teleportation Movement

In the *TeleportMovement* scene, teleport around the scene with the Sample Framework's *PlayerController* prefab.

1. Add the *PlayerController* prefab, which comes with the *OVRCameraRig* and a *LocomotionController*.
   > This prefab is in `Oculus/SampleFramework/Core/Locomotion/`.

2. Configure teleportation settings with the **Locomotion Teleporter** script in the inspector.
   > This is in the *LocomotionController* object of the *PlayerController*.
   >
   > By default, the *PlayerController* allows for linear movement, snap rotation, and teleportation. You can use the *Enable Movement/Rotation* options in the inspector to change this.

3. Choose which scripts will be active in the *LocomotionController* object to customize behavior.

#### Options
The *LocomotionController* has a lot of scripts! The controller should have one script from each of the following categories enabled. Feel free to experiment with different setups!

- **Teleport Input Handler**
  - **Teleport Input Handler HMD** - Player can aim teleports with their head.
  - **Teleport Input Handler Touch** - Player can aim teleports with their controllers.
    > Here you can also customize input options, like which buttons are used to teleport.

- **Teleport Aim Handler**
  > Both options will use the **Teleport Aim Visual Laser** script to visualize the aim.
  - **Teleport Aim Handler Laser** - Player's aim will follow a straight line.
  - **Teleport Aim Handler Parabolic** - Player's aim will follow a curved parabola.

- **Teleport Target Handler**
  > For all of the Target Handler scripts, there is an *Aim Collision Layer Mask* setting in the inspector. Make sure that this is set to a layer and that your intended teleportation destination(s) are also in this layer, otherwise the target will not be found.
  - **Teleport Target Handler Nav Mesh** - Player will only be able to teleport to spots on a [**NavMesh**](https://docs.unity3d.com/ScriptReference/AI.NavMesh.html).
  - **Teleport Target Handler Node** - Player will only be able to teleport to colliders that have a **Teleport Point** script.
    > For this option, see the *TeleportPoint* prefab in `Oculus/SampleFramework/Core/Locomotion/`.
  - **Teleport Target Handler Physical** - Player will be able to teleport to any physical collider.

- **Teleportation Orientation Handler**
  - **Teleportation Orientation Handler 360** - Does not consider rotation.
  - **Teleportation Orientation Handler HMD** - Player's rotation depends on their headset rotation.
  - **Teleportation Orientation Handler Thumbstick** - Player can adjust their teleport orientation by rotating the thumbstick.

- **Teleport Transition**
  - **Teleport Transition Instant** - The player teleports instantly with no transition.
  - **Teleport Transition Blink** - The player's screen should fade to black and fade back during the teleport.
  - **Teleport Transition Warp** - The player will quickly move to their destination, being able to see the teleport move them in the world.

### UI Raycast Interactions

To interact with UI elements like buttons and sliders, 
the Oculus Integration Package has an **OVR Input Module** to handle controller selections, and
an **OVR Raycaster** to attach to the canvases with UI elements.

1. Add the **OVR Raycaster** script to any canvas that has interactive elements.
    > You may have multiple canvases and multiple **OVR Raycaster**s in a single scene.
2. Set up the **OVR Input Module**
    > There should only be one of these per scene.
    >
    > There should also only be one **Event System**,
    > so if Unity automatically created one when you created your canvas, delete that one.
    >
    > The easiest way to get everything right is to use the *UIHelpers* prefab from the *SampleFramework* part of the Oculus Integration Package in `Oculus/SampleFramework/Core/DebugUI/Prefabs/`.

#### Options

- Change which buttons count as "clicking" the UI with the *Joy Pad Click Button* option in the inspector of the **OVR Input Module**.
  > This is under the *EventSystem* object of the *UIHelpers*.
- Change the color of the laser pointer with the *Debug Draw Line* material in the *LaserPointer*.
  > This is under the *LaserPointer* object of the *UIHelpers*. You may have to click an arrow next to the material to change the color.
  > <img width="1000" alt="LaserPointer" src="https://github.com/AlexWills37/UnityQuest2020Template/assets/77563588/b115b912-5dd3-4f93-92d0-4d2b53229926">

- Change the behavior of the laser pointer with the **SetLaserBehavior** script.
  > Attach this script to the *LaserPointer* object with the **LaserPointer** script to access the behavior variable.
  >
  > **On** - the raycast for selecting objects is always visible.
  >
  > **Off** - the raycast for selecting objects is never visible.
  >
  > **On When Hit Target** - the raycast for selecting objects is only visible when the ray is hitting a UI element with *Raycast Target* enabled.
- Change the cursor with the **Laser Pointer**'s *Cursor Visual*.
  > By default, this is the *Sphere* object that comes with the *UIHelpers* prefab.

## The rest of the Oculus Integration Package
You may wish to explore the rest of the Oculus Integration Package! Most of the package has been ignored from this repository to save space. In particular, this project only includes the following modules:
- VR
- Sample Framework (partial)
  - Core (partial)
    - Custom Hands
    - DebugUI
    - Locomotion

In particular, you may wish to check out the sample scenes in the Sample Framework folder `Oculus/SampleFramework/Usage/`.

To access the rest of the Oculus Integration Package, you will have to download and import it.

1. Download **v50.0** of the [**Oculus Integration Package**](https://developer.oculus.com/downloads/package/unity-integration/50.0/).
   > You should end up with a file `OculusIntegration_v50.0.unitypackage`.
2. Open the Unity Project.
3. In the menu bar at the top, navigate to **Assets > Import Package > Custom Package...**
4. Locate and select the `OculusIntegration_v50.0.unitypackage` you downloaded.
5. Follow any on-screen prompts to import the package and clean up any settings.

If you end up using assets from other parts of the Oculus Integration Package, make sure to change the `.gitignore` to stop ignoring them. 
