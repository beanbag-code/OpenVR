Hey all!
Welcome to the OpenVR project.
The goal of this project was to make a custom VR headset and allow it to work with X-Plane 12 on MacOS.
Very specific, I know.
Here is a video showcasing what it looks like.

https://vimeo.com/1213110818?share=copy&fl=sv&fe=ci

Here is a picture of the finished project.

<img width="3024" height="4032" alt="IMG_5685" src="https://github.com/user-attachments/assets/3d51aca2-0fe9-4119-b64f-b5d0660534bd" />


Before we begin I will give you a overveiw of the structure of this project.
First we have the hardware, there is the bill of materials in which you can buy the nessisary components.
The rest is 3D printed.

The software side is where things get intresting.

To understand you must first understand the limitations.
First of all, macOS does not natively support VR Rendering. So the option in X-Plane to render for a headset does not even exsit on Mac.
Next, the most poular app for interfacing with X-Plane is OpenTrack. From What I saw it is natively for Windows.
I did not try to get it to work on Mac, it might be posible, but I opted to make my own tracking code.

Now that you understand these limitations, here are all the parts for the software. I will list them in runtime order.
First the Audrino with the MPU records the rotation of the head and sends it over serial to the computer.
It is recived by the program VRTrack. VRTrack takes the data, corrects it and sends it over UDP port to X-Plane 12.
In my origninal idea, VRTrack would use AprilTag detection for drift coreection, however the IMU I chose drifts little, so I just commented it all out.
It is still mostly there if you want it back.

Next X-Plane recoves the data and turns the pilot's head in the sim accordingly. It then just renders the scene like normal.
In the background there is a app running called FreeVR. it records the screen, and then applies lens corections and makes it so that it shows two eyes.
The window for FreeVR is put full screen onto the VR headset screen where it is veiwed through lenes.

Got all that?


Alright so here is how you build your own headet.
First reveiw the Bill Of Materials and purchuse all the parts.
<img width="4032" height="3024" alt="IMG_5944" src="https://github.com/user-attachments/assets/c4421f6e-30af-4631-a5c3-acf8221b2306" />

Next print 1x Light-Hood, 1x Main-body, 1x Screen-Holder, 2x Lens-Holders, 1x Arduino-Holder, 1x Lid, and at least 4x Strap-Holders in PLA/PETG.
<img width="4032" height="3024" alt="IMG_5942" src="https://github.com/user-attachments/assets/f455fb6b-41d7-4287-abd1-b9f3a21952d2" />


Next print the Eye-Mask in TPU. (Note: This part been specificaly desgined to fit my face, if you wish to customize it for yourself, use the Fusion-360 file to edit to model. I photoscanned my face and used the 3d model to cut out the shape. You could feasibly do the same.)
<img width="3024" height="4032" alt="IMG_5943" src="https://github.com/user-attachments/assets/bd9ee244-b9ee-47aa-935f-06b10d849f49" />

Once you have all the parts, you are ready to assemble.
<img width="3024" height="4032" alt="IMG_5941" src="https://github.com/user-attachments/assets/1cc5f8ee-68fc-4a89-ab58-0a814faea4cf" />

Here is what fastening peices you will need.
![Uploading IMG_5944.JPG…]()
<img width="4032" height="3024" alt="IMG_5945" src="https://github.com/user-attachments/assets/0c04f323-e1f3-48ad-858c-9521c13e7362" />


First put the screen into the screen holder. Use the screws that came with the screen to secure it from the back.

<img width="4032" height="3024" alt="IMG_5946" src="https://github.com/user-attachments/assets/5fb39dbc-0b5c-4490-aea7-fa9917e291ba" />


Next put the lenses into the Lens-Holders, they rely on the plastic's elasticy to hold the lens in.
(NOTE: You will need to forceably modify the Lens-Holder peices, by cutting off the square tabs by the gaps. This will leave you with a C shaped circle.)

<img width="3024" height="4032" alt="IMG_5947" src="https://github.com/user-attachments/assets/f44f07e7-fada-4952-88cc-b52d18087978" />


Next put 3 M3 16mm screws through the bottom of the Lens-Hood in order that their threads are pointing up like such.
<img width="3024" height="4032" alt="IMG_5948" src="https://github.com/user-attachments/assets/ab99fcde-0f7f-44dc-a039-b950fc447c78" />


Place M3 washers on the screws in order to change the distance from screen to lens. I used 3 to start, you can ajust later.
<img width="3024" height="4032" alt="IMG_5949" src="https://github.com/user-attachments/assets/1b6acf92-0149-48ef-8539-a6697f1e0b0b" />

Next line up the holes of the Lens-Holder with the screws and put them on. Depending on your print tollerance, you might need to make the holes larger or go from beloow and screw it on. With enough time they will go on.
<img width="3024" height="4032" alt="IMG_5950" src="https://github.com/user-attachments/assets/bd060c2b-8f3c-41eb-83ac-c38ac861004d" />

Next use the M3 nuts on the remaining treadlenth for extra security. This is optional if it already fits tight, but is recomended.
<img width="3024" height="4032" alt="IMG_5951" src="https://github.com/user-attachments/assets/3028e985-719b-4481-9b4f-92b818ebe298" />

Next place the Light-Hood into the Main-Body and then place the Screen-Holder onto the top to sandwich the Lens-Hood between the two peices. Use 4x M3 16mm screws to screw the parts togerther. Be careful to note the direction the cords extend, In the image I put it so the screen's cords will go up. It will also take a consoderable amount of pressure for the screws to go in. It is possible self tapping screws will be easier than flat screws like I used.
<img width="3024" height="4032" alt="IMG_5952" src="https://github.com/user-attachments/assets/036566ca-f7a9-4085-868f-69b62fed9f82" />


Next we will work on the Arduino. Solder the headers onto the Nano and the IMU. then solder those parts onto a protoboard and conect the parts. Here is the pinout needed. 

NANO -> IMU
D9 ->   RST
D8 ->   INT
A4 ->   SDA
A5 ->   SCL
3.3v -> VCC
GND ->  GND

Here is what my final product looked like, the exact placement doesnt matter much, only that the pins are connected right.
<img width="3024" height="4032" alt="IMG_5953" src="https://github.com/user-attachments/assets/9d300762-28cb-4020-875b-3cf727279682" />


Next take the finished product and place it into the Ardrino-Holder. You may need to modify the part using something sharp in order to make sure whatever cable you use for the Nano will reach it. As you can see from my photo, I had to cut the wall a bit.
<img width="3024" height="4032" alt="IMG_5954" src="https://github.com/user-attachments/assets/54745aa3-11bc-4e42-a031-d0dfd64306d4" />

Next place the Lid-Part on top and secure it with M2x4mm screws. Again you may need to modify the lid, test the cabe to ensure a fit.
<img width="3024" height="4032" alt="IMG_5955" src="https://github.com/user-attachments/assets/93d78c6c-3c34-46b4-888d-ebe67bbccc35" />


After all that, we are going to put on the strap, here is where I would recommend you change my design, I used some straps that I found around the house. Elasic straps will probally be a ton more comfortable.

Once you have straps feed one longer strap through the bottom of the Arduino-Holder
<img width="3024" height="4032" alt="IMG_5956" src="https://github.com/user-attachments/assets/5d9a0fd8-6ac0-4533-bc2c-3cc8668aa843" />

Use two of the Strap-Holders to sequre the strap around the two side loops on the Main-Body.
<img width="3024" height="4032" alt="IMG_5956" src="https://github.com/user-attachments/assets/6e5e8d42-2a75-474e-a450-37f5978298bc" />

Next use the other two Strap-Holders and a strap to loop the two top loops on both the Main-Body and Arduino-Holder Parts.
<img width="3024" height="4032" alt="IMG_5958" src="https://github.com/user-attachments/assets/24895e06-aaa7-4ccb-816f-01410729027e" />


Again, I say, if anywhere you are going to modify my design, I would recomend this part. It works and that is it.

Next use take a magnet and push it into each hole of the Face-Mask peice, then keeping in mind the poliriation do the same for the Main-Body peice. as a result you should be able to attach the Face-Mask to the Main-Body using the magnitism.
<img width="4032" height="3024" alt="IMG_5961" src="https://github.com/user-attachments/assets/3fbfd226-3208-4912-9f38-69c1e16a999b" />
<img width="4032" height="3024" alt="IMG_5960" src="https://github.com/user-attachments/assets/92d55fd1-dbe5-44f4-b24d-f0c1a8e203d1" />
<img width="3024" height="4032" alt="IMG_5959" src="https://github.com/user-attachments/assets/1e7be326-2167-4eb5-ab44-b1952b1a1d18" />


Finaly, ajust the straps to your head.
Congrats, it has been fully assembled.

Next we will set up the software. download all the files. 

First flash the Ardrino using any IDE that connects to Ardrino. 
I recommend Ardino IDE as it is simplest. To test, check the serial monitor, you should see many lines of numbers streaming fast that change when you turn the device.

Next boot up VRTrack.
VRTrack relies on a few dependancies. Using homebrew run this command in the terminal. (brew install opencv glfw apriltag) Then go to the IMGui Github download the project and add it to your project folder.

I would recommend building the project youself. This means using CMake. Look up a tutorial to do so.

Once you have VRTrack up and running use the dropdwon to select your Arduino from the ports. Make sure no other appication is conneced to the Arduino, inculding Arduino IDE.

Click start and then hit calabrate in order to center the head using that direction.

Boot up X-Plane-12, go to the network tab and enable use UnPvP for Port Forewarding in the UDP ports section.
<img width="723" height="678" alt="Screenshot 2026-07-26 at 3 38 43 PM" src="https://github.com/user-attachments/assets/7eeb9388-03cf-4b6d-8bb2-40fb20832fa1" />

When you boot up a flight you should see that you can now control the head turn with the Arduino.

Use the calibrate to center it if it ever drifts.


Next plug in the HDMI display into your HDMI port.
(Note, I found that this LCD module is quite finicky, I recomend only direct HDMI conections, no USB-c adapters. Even then I found I needed to use a program called Better Display and basicaly reflash the EDID to get it to work. If you are having issues I wish you luck. I would recommend using AI to help you troubleshoot.

Finaly open the FreeVR App and allow screen recording and put the window onto the display's area, put it into full screen and then fly.

I hope that covers everything. I do not doubt there are issues somewhere, I have only tested it on my M3 Macbook Pro.
This project is not at all intended for everyone. I made it to chalange myself. That being said if you can use any of this, go right ahead. I will love you hear if you do end up making/using any of this.

Notes on the AI use. The FreeVR app is entirely vibe coded. I roughly understand how to funtions, but I do not know swift and shaders, so if I built it myself, I would have spent years. as for VRTrack, I did use AI estenively to understand the new systems, but I did write to code myself, using AI only where my knowlage was lacking.
