# ⛔️ DEPRECATED

This repo is deprecated and will no longer be maintained. Please visit Microchip's AVR and PIC git resources for up-to-date information: https://github.com/microchip-pic-avr-solutions

Information below is for archival purposes only, and may be removed at any point.

---

<p align="center">
    <a href="https://www.microchip.com/">
        <img src="https://storage.googleapis.com/avr-iot-media/microchip_round_logo.png" alt="Microchip logo" width=72 height=72 />
    </a>
    <a href="https://cloud.google.com/">
        <img src="https://storage.googleapis.com/avr-iot-media/cloud-logo.png" alt="GCP Logo" width=91 height=72 />
    </a>
    <a href="https://www.leverege.com">
        <img src="https://storage.googleapis.com/avr-iot-media/lvg-logo.png" alt="Leverege logo" width=72 height=72 />
    </a>
    <h2 align="center">PIC-IoT Quick Start</h2>
    <p align="center">
        A rapid deployment tool for getting your PIC-IoT data on the cloud. Powered by Leverege.
        <br>
        <a href="https://www.leverege.com/contact-us"><strong>Talk to an Expert »</strong></a>
        <br>
        <br>
    </p>
</p>

(Links will open in this window. Shift+click, command+click, or middle mouse click to open in new window or tab.)

## Table of Contents
1. [Set up your GCP and Firebase Projects](#set-up-your-gcp-and-firebase-projects)
3. [Run the Quickstart Script](#run-the-quickstart-script)
4. [Add your devices public key to your IoT Core Registry](#add-your-device-public-key-to-your-iot-core-registry)
5. [Update your PIC-IoT device firmware](#update-your-pic-iot-device-firmware)

##

This repository contains resources for quickly connecting your [PIC-IoT device](https://pic-iot.com/) to your own Google Project and deploying a live UI to Firebase.

Following this guide, you will clone this repo into your Google Cloud project, and run a script that:
* enables [Cloud Functions](https://cloud.google.com/functions/docs/), [Cloud IoT Core](https://cloud.google.com/iot-core/), and [Pub/Sub](https://cloud.google.com/pubsub/), 
* creates a `pic-iot` Pub/Sub topic,
* creates an IoT registry (default name: `PIC-IOT`, configurable in the script),
* adds your device's UID to the registry,
* builds and deploys a Cloud Function to route Pub/Sub messages to your [Firebase project](https://firebase.google.com/), and
* builds and deploys a UI to firebase.

After running the quick
script, you'll need to add your device's secure pubkey to the device's entry in your IoT core registry and update the firmware on your device using MPLAB Code Configurator. 

## Set up your GCP and Firebase Projects

The quickstart requires that you have a Firebase project connected to a GCP project with billing enabled.

### GCP Project

1. Create (or select an existing) GCP project.    

    <a href="https://console.cloud.google.com/cloud-resource-manager" target="_blank">GO TO THE MANAGE RESOURCES PAGE</a>

2. Enable billing for the project.

    <a href="https://cloud.google.com/billing/docs/how-to/modify-project" target="_blank">LEARN HOW TO ENABLE BILLING</a>

### Firebase Project

1. Launch the Firebase Console.

    <a href="https://console.firebase.google.com/u/0/" target="_blank">GO TO FIREBASE CONSOLE</a>

2. Select 'Add project'.

    <img src="https://storage.googleapis.com/avr-iot-media/fb-add.png" height="100">

3. In the Project Name field, select the GCP project you created or selected above.

    <img src="https://storage.googleapis.com/avr-iot-media/fb-connect.png" height="100">

4. Click 'Add Firebase'.

## Run the Quickstart Script

1. Open [Cloud Shell](https://console.cloud.google.com) from your project.

    <img src="https://storage.googleapis.com/avr-iot-media/cloudshell.png" height="80">

2. In the shell, run 

```bash
git clone https://github.com/Leverege/microchip-pic-iot.git && cd microchip-pic-iot/setup && bash setup.sh
```

   to clone this repo, enter the newly created directory, and run the quickstart script.

3. You will need to provide firebase authentication. To do this, copy the authentication URL provided in the shell console, and paste it into a new browser window. Then, log in on that page, authorize the app, and copy the security key. Paste the security key into the shell at the prompt and hit return.

4. At the prompt, enter your PIC-IoT device's UID. Your device's UID is the last portion of the url you see after launching CLICK-ME.HTM from the device. 

    <img src="https://storage.googleapis.com/pic-iot-media/device_uid.png" height="30">

5. If you would like to customize your IOT Core registry name, you may do so at the IoT core registry name prompt.

    IoT core registry names must start with a letter, use only letters, numbers, hyphens, and the following characters:

        + . % _ ~

6. The setup script will run for several minutes.
    The setup script will:
    * Enable Cloud Functions, IoT Core, and Pub Sub in your GCP project
    * Create an IoT Core registry called PIC-IOT and register your device
    * Install, build, and deploy Cloud Functions and the UI

## Add your device public key to your IoT Core Registry

1. Make sure your device is connected to your computer via USB.

2. Open your IoT Core registry management page, and select the PIC-IOT registry.

    <a href="https://console.cloud.google.com/iot/registries" target="_blank">OPEN IOT CORE REGISTRY MANAGEMENT</a>

3. Click on your device's UID in the list.

    Because registry entries must begin with a letter **your device UID will be prefixed with a 'd'**. To search for your device by uid, you must enter 'd<your_device_id>' in the search box.

4. Click the **Add public key** button.

    <img src="https://storage.googleapis.com/avr-iot-media/iotcore-addpub.png" height="70">

5. Select 'Upload' under the input method, and ES256 (**not** ES256_X509) as the public key format. Then click the **Browse** button.

    <img src="https://storage.googleapis.com/avr-iot-media/iotcore-addauthkey.png" height="150">

6. In the upload window, navigate to the CURIOSITY drive, then select PUBKEY.TXT and click add to upload it. 
    
    <img src="https://storage.googleapis.com/avr-iot-media/iotcore-click-add.png" height="150">
    
## Update your PIC-IoT device firmware

1. Follow the PIC-IoT documentation for updating your PIC board's firmware with your new GCP project information using MPLAB Code Configurator.

## View your live data!

And that's it! If you've edited your device with the MPLAB, you should see live data flowing to your new Firebase app at \<your-project-id\>.firebaseapp.com/device/\<your-device-uid\>. 

## Building a solution at scale? 
<p> 
        Want to build something bigger? We can help you scale your projects into solutions. <a href="https://www.leverege.com/form/contact-us"><strong>Talk to an IoT expert.</strong></a>
</p>
<p> 
       Whether you're a Fortune 500 company or startup, transforming your current business or creating entirely new businesses, it takes a team with deep experience across verticals and use cases to turn your IoT prototype into an IoT product.
</p>
<p align="center"> 
   <img src="https://storage.googleapis.com/avr-iot-media/lvg-logo-wide.png" height="25">
    </p>
