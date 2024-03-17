# First Time Setup
<!-- This file is meant to be viewed online on GitHub or in a markdown reader -->
Welcome to developing Unity games for the Quest 2 headset! This guide is intended to go through all the necessary steps to get started developing, particularly with **Unity 2020.3.48**.

By the end of this setup, you should be able to build and run this template project on the Quest 2 headset!

There are 3 main components to this setup:

- [Preparing your computer to build and send apps](#preparing-your-computer)
- [Preparing the Quest 2 headset to receive apps](#preparing-the-quest-2)
- [Checking the device list](#checking-the-device-list)

**Also, if you use this template, follow the steps in [this setup section](#setting-up-a-new-application-with-the-template)! Otherwise the app might not build to the headsets.**
> This template app will be built to the school headsets from my computer, so you need to change the project's package name or it will conflict and possibly not build.

## Preparing your computer
On your computer, you will need
- [Unity 2020.3.48](https://unity.com/releases/editor/whats-new/2020.3.48)
  - Android Build Support module
  - Android SDK & NDK Tools module
  - OpenJDK module

- (Windows only) [Oculus ADB Drivers](https://developer.oculus.com/downloads/package/oculus-adb-drivers/)
- A Unity project
  > It is recommended to download this repository and use this template project.

If you are missing these components, keep reading. If you already have Unity and the Oculus ADB Drivers (or if you have Unity on Mac/Linux), you can skip to [preparing the headset](#preparing-the-quest-2) or [checking the device list](#checking-the-device-list).

### Installing Unity
If you do not have the 2020 version of Unity installed, follow these steps:
1. Download the [Unity Hub](https://unity.com/download).
2. Go to this [Unity 2020.3.48 release page](https://unity.com/releases/editor/whats-new/2020.3.48).
3. Click *Install this version with **Unity Hub***.
4. When the Unity Hub opens and gives you the options, check off the boxes for:
   - Android Build Support
     - OpenJDK
     - Android SDK & NDK Tools
   > If you already have Unity 2020 installed but not the Android Build support modules, you can add them by going to the **Installs** section of the Unity Hub, right clicking the entry for Unity 2020, and clicking *Add Modules*.
5. Once the install is complete, try openning a Unity project such as the one in this repository.

### Installing drivers (Windows only)
If you are on Windows and have not installed the drivers already, follow these steps:

1. Download the [Oculus ADB Drivers here](https://developer.oculus.com/downloads/package/oculus-adb-drivers/).
2. Unzip the files.
3. Right-click the `android_winusb.inf` file.
4. Click **Install**.

## Preparing the Quest 2
If you are in Professor Roy's VR class, the school's headsets should already be setup and you can skip to **step 4**. If you have your own headset, you will have to enable **developer mode** and **USB debugging**, so keep reading.

By the end of this section, we should be able to see our headset in the device list when we open a Unity project, go to **File > Build Settings...** from the Menu Bar, switch the platform to Android, and click the dropdown next to *Run Device*. Read the [device list section](#checking-the-device-list) for more details.

The official instructions can be found [on Meta's developer site](https://developer.oculus.com/documentation/native/android/mobile-device-setup/), as they might change with updates. Generally speaking, the process is as follows:

(You can skip the first 3 steps if you are using the school headsets, since they are already in developer mode)

1. Create a Meta Developer account.
   > This account must be associated with an **organization** (you can create your own organization if you want), and it must be **verified** (2-factor authentication).
2. Log into this account on the headset.
3. Enable USB debugging.
   > You can try going to **Settings > System > Developer** like Meta's guide says, but sometimes this doesn't work, or the options aren't available. What you're looking for is an option to turn on **USB Connection Dialog**.
   >
   > The more reliable option is to connect to the headset with a smartphone:
   > 
   > 1. Download the Meta Quest Mobile App.
   > 2. Log into your developer account.
   > 3. Connect to your headset (Bluetooth required).
   > 4. From the app, go to **Headset Settings > Developer Mode** and enable **Debug Mode**.

4. Connect the headset to your computer through USB.
5. In the headset, you should see a dialogue box asking to allow USB debugging. Click *Yes*, or *Always allow from this computer*.
   > If you do not see the dialogue box appear, it may be possible that USB debugging is already allowed from this computer.
   >
   > If this is the case, check to see if the headset shows up in Unity's devices list (see the [device list section](#checking-the-device-list)).
   >
   > If the dialogue box does not show up, AND the headset does not show up in the deivce list, double check that developer mode is enabled with the mobile app. For the school's headsets, the Motorola phones are connected with the Meta Quest App.
   >
   > If the headset is still not registering as a device, and you are on Windows, double check that you installed the [Oculus ADB Drivers](https://developer.oculus.com/downloads/package/oculus-adb-drivers/).
   ![Image](https://scontent.ftpa1-1.fna.fbcdn.net/v/t39.2365-6/123501957_688453455418503_2729454915805133542_n.png?_nc_cat=110&ccb=1-7&_nc_sid=e280be&_nc_ohc=-2gGvs3b-GwAX_ID2xt&_nc_ht=scontent.ftpa1-1.fna&oh=00_AfAzOmR_ug-Fssq3zmV2brP_GXu7QS-PgGPMEOzQufYidA&oe=66108785)

## Checking the device list
Check the device list to see if your apps can be built to the headset!

1. Open a Unity project.
2. In the menu bar, navigate to **File > Build Settings...**
3. Switch the platform to **Android**.
4. Next to *Run Device*, click on the dropdown.
5. You should see something like **Oculus Quest 2 (\<Device ID\>)**.
   <img width="555" alt="Device List in the Build Settings window" src="https://github.com/AlexWills37/UnityQuest2020Template/assets/77563588/358099bf-c55b-418b-b48d-91d893cc1595">

7. If the device isn't showing, click **Refresh**.
8. If the device still isn't showing, double check the following:
   
   - The headset is connected to the computer.
   - In the headset, you clicked *Allow USB Debugging*, or you clicked *Always allow from this computer* before.
     - If the dialogue doesn't appear, check if developer mode is enabled using the mobile app.
   - If you're on Windows, you installed the [Oculus ADB Drivers](https://developer.oculus.com/downloads/package/oculus-adb-drivers/).

At this point, if the device is showing up, you can build apps the the headset! There are still a few steps to make your game VR compatible, so keep reading for details on setting up new applications.


## Setting up a new application with the template
If you've setup your computer and the headset correctly, you can now build the template to the headset! You may run into a few issues though, so please follow these steps.

1. Download, clone, or fork this repository.
2. Rename the main folders for your project's name.
3. Set up your GitHub repository, making any changes necessary.
4. Open the Unity project folder with Unity 2020.
5. In the menu bar, navigate to **Edit > Project Settings...**
6. Navigate to the **Player** tab of the settings.
7. Change the *Company Name* and *Product Name* for your project.
   <img width="839" alt="Player settings with the Company and Product names" src="https://github.com/AlexWills37/UnityQuest2020Template/assets/77563588/ed2c2e76-1994-4980-be91-6d7a63ad43ab">

9. Scroll down to the **Other Settings** section (inside of the **Player** tab).
10. Make sure that *Override Default Pacakge Name* is set to false, or that the
   *Package Name* is unique to your project.
   > If the package name matches a project that is already installed on the headset (like this template, `com.NCF.UnityQuest2020Template`),
   > and the project is built from a different computer, it will **NOT** install the project to the headset.
   <img width="842" alt="Package Name Override setting" src="https://github.com/AlexWills37/UnityQuest2020Template/assets/77563588/5cc3a73e-6229-49f4-8cb2-826aa4eb1080">


## Setting up a project from scratch
This kind of defeats the purpose of the template project, but if the template isn't working, here is how to set everything up from scratch. This takes a long time to import and reimport as the settings change.

These steps are simplified from [Meta's official tutorial for Unity](https://developer.oculus.com/documentation/unity/unity-tutorial-hello-vr/).

1. Create a Unity project.
2. Import the SDK.
   > Meta now has an all-in-one SDK in the asset store, but it is not compatible
   > with Unity 2020. This template project uses the [**Oculus Integration Package v50.0**](https://developer.oculus.com/downloads/package/unity-integration/50.0).
   >
   > To import this package, download the `.unitypackage` file from the link above.
   >
   > Then navigate in the menu bar: **Assets > Import Package... > Custom Package...**
   >
   > Import the `.unitypackage` file for the Oculus Integration Package. This will take some time!
3. If prompted, accept Unity's suggestions and restart the window if needed.
4. Switch the build platform to **Android** by going to **File > Build Settings...**, clicking **Android**, then **Switch Platform**.
5. Navigate to **Edit > Project Settings...**
6. Go to the **Oculus** tab.
7. Click **Fix All** under the **Outstanding Issues** tab.
8. Click **Apply All** under the **Recommended Items** tab.
   > ![Oculus settings with the Fix and Apply All buttons](https://private-user-images.githubusercontent.com/77563588/292604196-b57f78da-7810-4ec4-9eaf-6c65430fb591.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3MTA2MzI4MjcsIm5iZiI6MTcxMDYzMjUyNywicGF0aCI6Ii83NzU2MzU4OC8yOTI2MDQxOTYtYjU3Zjc4ZGEtNzgxMC00ZWM0LTllYWYtNmM2NTQzMGZiNTkxLnBuZz9YLUFtei1BbGdvcml0aG09QVdTNC1ITUFDLVNIQTI1NiZYLUFtei1DcmVkZW50aWFsPUFLSUFWQ09EWUxTQTUzUFFLNFpBJTJGMjAyNDAzMTYlMkZ1cy1lYXN0LTElMkZzMyUyRmF3czRfcmVxdWVzdCZYLUFtei1EYXRlPTIwMjQwMzE2VDIzNDIwN1omWC1BbXotRXhwaXJlcz0zMDAmWC1BbXotU2lnbmF0dXJlPTMyMGQxM2NiNDhjNDNiOGNjMTQ1ZDcxNDdhYTY3MDkwMzkwZTI1NWM3YTE1MWI2OTc0MzJjZTQwODhkOWU3YjgmWC1BbXotU2lnbmVkSGVhZGVycz1ob3N0JmFjdG9yX2lkPTAma2V5X2lkPTAmcmVwb19pZD0wIn0.UWHN4sQR2T0TY_yU-DPRnblNTk19NhUipRvQBq1O_2M)
10. Add the *OVRCameraRig* prefab to the scene instead of the *Main Camera*
11. Try building the app to the headset!
