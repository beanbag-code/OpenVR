Hey all!
Wecome to the OpenVR project.
The goal of this project was to make a custom Vr headset and allow it to work with X-Plane 12 on MacOS.
Very specific, I know.

Before we begin I will give you a overveiw of the structure of this project.
First we have the hardware, there is the bill of materials in which you can buy the nessisary components.
The rest is 3D printed.

The software side is where things get intresting.

to understand you must first understand the limitations.
First of all, macOS does not natively support VR Rendering. So the option in X-Plane to render for a headset does not even exsit on Mac.
Next, the most poular app for interfacing with X-Plane is OpenTrack. From What I saw it is natively for Windows.
I did not try to get it to work on Mac, it might be posible, but I opted to make my own tracking code.

Now that you now these limitations, here are all the parts for the software. I will list them in runtime order.
First the Audrino with the MPU records the rotation of the head and sends it over serial to the computer.
it is recived by the program VRTrack. VRTrack Takes the data and corrects it and sends it over UDP port to X-Plane 12.
In my origninal idea VRTrack was going to use AprilTag detection for drift coreection, however the IMU I chose drifts little, so I just commented it all out. 
It is still mostly there if you want it back.

Next X_plane recoves the data and turns the pilot's head in the sim accordingly. it then just renders the scene like normal.
In the background there is a app running called FreeVR. it records the screen, and then aplys lenscorections and makes it so that it shows two eyes.
The window fo FreeVR is put full screen onto the VR headset screen where it is veiwed through lenes.

Got all that?
