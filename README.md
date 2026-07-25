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


Alright so here is how you build your own headet.
First Reveiw the Bill Of Materials and purchuse all the parts.
Next print 1x Light-Hood, 1x Main-body 1x Screen-Holder and 2x Lens-Holders in PLA/PETG.
Next print the Eye-Mask in TPU. (Note: This part been specificaly desgined to fit my face, if you wish to custimise it for yourself, use the fusion 360 file to edit to model, Scan your face and replace my face scan with yours.)

Once you have all the parts you are ready to assemble.
First put the screen into the screen holder. Use the screws that came with the screen to secure it from the back.

Next put the lenses into the Lens-Holders, it rellys on the plasitics elasticy to hold the lens in.

Next use ######## to screw the Lens-Holder onto the Light-Hood.
Place washers between in order to change the distance from screen to lens. I used 3 to start, you can ajust later.

Next place the Light-Hood into the Main-Body and then place the Screen-Holder onto the top to sandwich the Lens-Hood between the two peices. Use %%%%^$*&W^&* to screw the parts togerther.

Next we will work on the ardrino. Solder the headers onto the nano and the IMU. then solder those parts onto a protoboard and conect the parts. Here is the pinout needed. 

NANO -> IMU
D9 ->   RST
D8 ->   INT
A4 ->   SDA
A5 ->   SCL
3.3v -> VCC
GND ->  GND

Here is what my final product looked like, the exact placement doesnt matter much, only that the pins are connected right.

Next take the frinished product and place it into the Ardrino-Holder. you may need to modify the part using something sharp in order to make sre whatever cable you use for the Nano will reach it.
Next place the Lid-Part on top and secure it with #### screws.

After all that, we are going to put on the strap, here is where I would recomed you change my desing, I used some straps that I found around the house. Use the Strap-Part in oreder to find a way to secure all the straps around like this picture.

After it has been secured, ajust to your head and set the spraps. Congrats, it has been fully assembled.
Next we will set up the software. downlaod all the files. First Flash the ardrino using any IDE that connects to ardrino. I recommend Ardino IDE as it is simplest. To text, check the serial monitor, you should see many lines of numbers streaming fast that schange when you turn the device.

Next boot up VR Track and X-Plane. In VRTrack use the dropdwon to select your ardrino from the ports. Make sure no other appication is conneced to the ardrino, inculding ardrino IDE.

Click start and then hit calabrate in order to center the head using that direction.

Go into X-Plane-12, go to the network tab and enable use UnPvP for Port forewarding in the UDP ports section.
When you boot up a flight you should see that you can control the head turn with the ardino.

Use the calibrate to center it if it ever drifts.

plug in the hdmi display into your HDMI port.
(Note, I found that this pertucular module is quite finnicy, I recomend only direct HDMI conections, no USB-c adapters. Even then I found I needed to use a program called better display and basicaly reflash the EDID to get it to work. If you are having issues comment and I can try to figure it out with you.)

finaly open the FreeVR App and allow screen recording and put the window onto the display's area, put it into full screen and then fly.

I hope that covers everything. I do not doubt there are issues somewher, I have only tested it on my M3 Macbook Pro.
This project is not at all ment for everyone. I made it to chalange myself. that being said if you can use any of this, go right ahead.
Notes on the AI use. The FreeVR app is entirely vibe coded. I roughly understand how to funtions, but I do not know swift and shaders, so if I built it myself, I would have spent years. as for VRTrack, I did use AI estenively to understand the new systems, but I did write to code myself, using AI only where my knowlage was lacking.
