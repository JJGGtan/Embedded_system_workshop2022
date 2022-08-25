<img src="https://raw.githubusercontent.com/JJGGtan/ICT_workshop2022/main/icon_ict2.png">

# Hi all, welcome to Thailand-Japan Student ICT Workshop 2022 repository :robot: :smile_cat: :desktop_computer:
### *A hands-on tutorial on hand gesture recognition for hardware control* 

###  22 December 2022
#### *by Robotic Engineering and Artificial Intelligence (REAI), Faculty of Engineering, Chiang Mai University*
---

> *This workshop is designed for those who are interested in integrating the microcontroller system with a machine learnign framework. Here, [MediaPipe](https://google.github.io/mediapipe/) is selected regarding its low computational resource requirement and simple implementation. To control microcontroller, [pyFirmata](https://pypi.org/project/pyFirmata/#:~:text=pyFirmata%20is%20a%20Python%20interface,Python%202.7%2C%203.3%20and%203.4.) is picked out to perform the serial communication between Arduino and Python. For the attendees' fullest advantages, this workshop requires:*
> 1. *A computer with a camera connected* ***(Attendees are responsible to bring this item)***
>2. *Arduino UNO R3 (Qty. 1)* ***(provided)***
>3. *USB square port data cable type B (Qty. 1)* ***(provided)***
>4. *Servo motor (Qty. 1)* ***(provided)***
>5. *Breadboard (Qty. 1)* ***(provided)***
>6. *Resistor (Qty. 5)* ***(provided)***
>7. *LED (Qty. 5)* ***(provided)***
>8. *Jumper wires* ***(provided)***
>
> *Attendees are also expected to complete installing the following softwares and libraries (regarding to the previously provided [guideline](https://colab.research.google.com/drive/1rvIae6hsvQDKnhotqOErPsn2PHxYOPm8?usp=sharing)).*
>
> <u><i>software</i></u>
>1. [*Arduino IDE*](https://www.arduino.cc/en/software)
>2. [*Visual Studio Code*](https://code.visualstudio.com/)
>
> <u><i>Python library</i></u>
>1. [*MediaPipe*](https://pypi.org/project/mediapipe/)
>2. [*OpenCV*](https://pypi.org/project/opencv-python/)
>3. [*pyFirmata*](https://pypi.org/project/pyFirmata/#:~:text=pyFirmata%20is%20a%20Python%20interface,Python%202.7%2C%203.3%20and%203.4.)

## ***Tool introduction***

#### <u>Arduino IDE</u>
Arduino IDE is the open-source Arduino Software which is designed for Arduino board users to make them capable to communicate with the hardware via coding, where IDE hereby stands for an integrated development environment which describing software for building applications that combines common developer tools into a single graphical user interface (GUI)[[1]](https://www.redhat.com/en/topics/middleware/what-is-ide#:~:text=An%20integrated%20development%20environment%20(IDE,graphical%20user%20interface%20(GUI) ). In most of the works, to simplify the program and workflow, we use a prior developed programming resource called <i><u>library</u></i> which is defined in computer science as a programming part including processes and subroutines (with or without source code) which are necessary in one specific program or software workflow. 

#### <u>Necessary python libraries</u>
<u><i>[pyFirmata](https://pypi.org/project/pyFirmata/#:~:text=pyFirmata%20is%20a%20Python%20interface,Python%202.7%2C%203.3%20and%203.4.) </u></i>

This is a library allows python users to communicate with microcontrollers via the [*Firmata*](http://firmata.org/wiki/Main_Page) protocol which is one of the communication protocol between microcontrollers and a host computer.

[*OpenCV*](https://pypi.org/project/opencv-python/)

Open Source Computer Vision Library (OpenCV) is a library designed for using in computer-vision to develope high-level applications such as face detection, feature matching and object tracking [[2]](https://dl.acm.org/doi/10.1145/2181796.2206309).

[*MediaPipe*](https://pypi.org/project/mediapipe/)

It is a library developed by Google used in detecting face, body gestures and object from a streaming media by utilizing machine learning model. In this workshop, we are also using [*MediaPipe Hands*](https://google.github.io/mediapipe/solutions/hands) which is a hand and fingers tracking solution provided by the library. With this solution, it is perhaps helpful to hereby introduce the *Hand landmark* model for better understanding. 

> ***Hand landmark model*** is the model identifying the key point location of 21 3D hand-knuckle coordinates. Each coordinate has a specific keypoint value, as shown in the following figure, to allow us to design the hand gesture recognition program. 
>
><img src="https://raw.githubusercontent.com/JJGGtan/ICT_workshop2022/main/materials/pics/hand_landmarks.png" width=500/> 
>
> *figure 1: 21 loacations in hand landmark model [[3]](https://google.github.io/mediapipe/solutions/hands)* 
>
> <img src="https://raw.githubusercontent.com/JJGGtan/ICT_workshop2022/main/materials/pics/hand_crops.png" width=500/> 
>
> *figure 2: Hand gestures examples [[3]](https://google.github.io/mediapipe/solutions/hands)*

## ***Section 0: Getting started***

In this section, we will introduce you to VS code basic operation and virtual environment creation.

<u><i> VS code workspace creation </u></i>

- Download .zip file from the workshop [repository](https://github.com/JJGGtan/ICT_workshop2022.git) by clicking `Download ZIP` as shown in the following figure. 
<img src="https://raw.githubusercontent.com/JJGGtan/ICT_workshop2022/main/materials/pics/git_download_zip.png" width="800px"> 

- Unzip the file and then launch VS Code software.
<img src="https://raw.githubusercontent.com/JJGGtan/ICT_workshop2022/main/materials/pics/VScode_launch.png" width="600px">

- Within unzipped folder named `"ICT_workshop2022-main"` by default, go to directory `ICT_workshop2022-main\ICT_workshop2022-main\materials\codes\ICT Project code and controller`. Select the folder named `"ICT Project code and controller"`.

- Now, in the VS code left vertical panel, there is a previously called folder appear. On the top bar, select `Terminal` and then select `New Terminal` as shown in the following figure. 
<img src="https://raw.githubusercontent.com/JJGGtan/ICT_workshop2022/main/materials/pics/New_terminal.png" width="600px">

- Here, the terminal will appear on the bottom section of the VS code window as shown in this figure. 
<img src="https://raw.githubusercontent.com/JJGGtan/ICT_workshop2022/main/materials/pics/terminal_appear.png" width="600px">

- At this point, you can now write a command to create a virtual environment containing file as noted in the pre-workshop manual or as follows.
```
python -m venv .venv source .venv/bin/activate
```

Then install the required libraries.
<li> <i><a href="https://numpy.org/">NumPy</a> : essential for performing mathematical operations </i> To do so, on the terminal, type
<code>python -m pip install numpy</code>
<li> <i><a href="https://matplotlib.org/">Matplotlib </a> : for data graphical visualization.</i> Type <code>python -m pip install matplotlib</code>
<li> <i><a href="https://pypi.org/project/opencv-python/"> OpenCV </a> : for real-time computer vision implementation </i> Type <code>python -m pip install opencv-python</code>
<li> <i><a href="https://pypi.org/project/mediapipe/"> MediaPipe </a> : for machine learning framework implementation </i> Type <code>python -m pip install mediapipe</code>
<li> <i><a href="https://pypi.org/project/pyFirmata/#:~:text=pyFirmata%20is%20a%20Python%20interface,Python%202.7%2C%203.3%20and%203.4."> pyFirmata </a> : for Python-Arduino serial communication </i> Type <code>python -m pip install pyFirmata</code>
</ol>

---
## ***Section 1: Hand-knuckle position identification using OpenCV and MediaPipe modules***

In this section, we are counting the number of the raised fingers by using the modules in OpenCV and MediaPipe library in python. In this part the aim is to get more familiar with:
- Camera manipulation via python
- Output format from MediaPipe Hands module
- Output processing and visualizing.

<u><i>1.1 Creating a video capture object </i></u>

After importing the `cv2` and `mediapipe` libraries, by using a command `video=cv2.VideoCapture(0)`, we can create a video capture object named "video". 

<u><i>1.2 Hand-knuckle coordinates positioning </i></u>

In the next step, we could analyze the captured video by reading the image from the video via a command `ret,image=video.read()` and then use the hand detecting model `mediapipe.solutions.hands` as a tool to detect a hand in the read image. 
At this point, we can identify hand-knuckle positions by using the command `mediapipe.solutions.hands.Hands.process(image)`. As a result, the 21 positions of the hand knuckles would be identified. Here in the example, we count the number of raised fingers by considering the relative position between the interesting index positions. 

<u><i>1.3 Result displaying</i></u>

To display the analysed result, we can use the command `cv2.rectangle(image, (20, 300), (270, 425), (0, 255, 0), cv2.FILLED)` to create a rectangle on the read image and the command `cv2.putText(image, str(total), (45, 375), cv2.FONT_HERSHEY_SIMPLEX, 2, (255, 0, 0), 5)` to display the variable `total` as a string format. Finally, we use the command `cv2.imshow("Frame",image)` to display the image with the text that is prior created. Furthermore, to exit the program execution, it is recommended to press `CTRL+c` on the terminal panel to stop and close the captured video window. 

<i><u> [Python Code example for finger counting program](https://github.com/JJGGtan/ICT_workshop2022/blob/dd571bea1d53213e891f9b2185db30c71b1c2fd9/materials/codes/ICT%20Project%20code%20and%20controller/LED/LED-test/LED-test.ino) </i></u>

---
## ***Section 2: Hand gesture controlled LEDs***

<u><i>2.1 LEDs control using Arduino IDE</i></u>

In this subsection, we are controlling 5 LEDs by creating a one-by-one on/off pattern. To turn on a LED, the input voltage is applied across the LED with a higher voltage source and the lower voltage source connected to the LED's anode (longer leg) and cathode (short leg), respectively. With Arduino, we could simply connect the anode to any digital input/output port and the cathode to the GND port as shown in figure 3. 

<img src="https://raw.githubusercontent.com/JJGGtan/ICT_workshop2022/main/materials/pics/LED.png" width=500/> 

*figure 3: Arduino Uno board and LEDs connection*


By uploading a command `digitalWrite(A, HIGH);`, the digital port number A will output a high digital signal equal to 5V for the Arduino Uno board. To switch the output from port number A to low (0V), we could use the command `digitalWrite(A, LOW);`. Furthermore, with Arduino, we could control each LED to turn on and off one-after-another by uploading the following code to the Arduino board.

<u><i>[Arduino source code for LED control](https://github.com/JJGGtan/ICT_workshop2022/blob/7e3ad26e69db2d3bca42e68546af040b167139c1/materials/codes/ICT%20Project%20code%20and%20controller/LED/LED-test/LED-test.ino)</i></u>


<u><i>2.2 LEDs control using hand gesture</i></u>

Firstly, to create a communication between arduino and python, on the Arduino board, we need to upload the example sketch named "StandardFirmata.ino" as shown in the following figure. 

<img src="https://raw.githubusercontent.com/JJGGtan/ICT_workshop2022/main/materials/pics/arduino_firmata.png" width=800/> 

*figure 4: StandardFirmata.ino launching*

Then, in the VS Code, compile the following [mainLED.py](https://github.com/JJGGtan/ICT_workshop2022/blob/9c9b762461aa3d0c734f64dbb8252fe68300e82c/materials/codes/ICT%20Project%20code%20and%20controller/LED/mainLED.py) file to launch the camera window and start receiving the input from the hand gesture. After compiling the code, try to show different hand gestures to the camera. We will see that the number of the turned-on LED would be the same as the number of your raised fingers. Note here that the main program works well with the controller.py file located in the same folder, since the led() function should be called from the controller.py file. In the file, we should set the comport variable to select the right communication port with Arduino.

<u><i>[Main openCV source code (LED)](https://github.com/JJGGtan/ICT_workshop2022/blob/7e3ad26e69db2d3bca42e68546af040b167139c1/materials/codes/ICT%20Project%20code%20and%20controller/LED/mainLED.py)</i></u>, 
<u><i>[LED controller source code](https://github.com/JJGGtan/ICT_workshop2022/blob/7e3ad26e69db2d3bca42e68546af040b167139c1/materials/codes/ICT%20Project%20code%20and%20controller/LED/controller.py)</i></u>

---

## ***Section 3: Hand gesture controlled servo motor***

In this section, we are using our hand gestures to control the rotating behaviour of a servo motor by controlling it to rotate to any specfic angle regarding our raised finger number. 

<u><i>Servo motor connection</i></u>

To drive the servo motor, it is required to connect the following color-labeled cables with the right Arduino ports;
1. Brown cable: connect to GND port,
2. Red cable : connect to 5V port,
3. Orange cable : connect to the digital pin number 9 (the port number could be change as to any port with PWM label)

<img src="https://raw.githubusercontent.com/JJGGtan/ICT_workshop2022/main/materials/pics/servo.png" width ="500px">

*Figure 5: Servo motor-Arduino connection*

<u><i>Example code for controlling the servo horn's position via hand gesture</i></u>

<u><i>[Main openCV source code (servo motor)](https://github.com/JJGGtan/ICT_workshop2022/blob/eca4ce956de5101503bdf5977ac6a283c73a6b2a/materials/codes/ICT%20Project%20code%20and%20controller/SERVO/mainSERVO2.py)</i></u>

Similar to the precious session, another controller.py file (as shown below) is required in order to call the function `servo()`.
<u><i>[Servo motor controller source code](https://github.com/JJGGtan/ICT_workshop2022/blob/eca4ce956de5101503bdf5977ac6a283c73a6b2a/materials/codes/ICT%20Project%20code%20and%20controller/SERVO/controller.py)</i></u>

---

## ***Workshop summary***

From the previous sessions, we have learned how to integrate the machine learning computer vision package in python with hardware controlling software, to create a computer vision controlled system with an assisting machine learning agent, which is the very first step of developing a higher-level application. Here are some examples:

<i><u> [Touchless object manipulation](https://create.arduino.cc/projecthub/norbertzare1/control-objects-like-a-jedi-232fc8?ref=tag&ref_id=gesture&offset=20) </u></i>

<img src="https://hackster.imgix.net/uploads/attachments/1430401/_0MnnJ2I5TH.blob?auto=compress%2Cformat&w=900&h=675&fit=min", width="500px">

*(Figure credit: https://create.arduino.cc/projecthub/norbertzare1/control-objects-like-a-jedi-232fc8)*

<u><i> [Intelligent service robot for people with disabilities or a limited range of movement](https://www.semanticscholar.org/paper/Comparisons-of-planar-detection-for-service-robot-Zhang-Huang/c1b02b251c68e8c3fd0ccdb16ad33f8769530afc)</i></u>

*An automatic moving, grasping and delivering task, the abilities of service robot dealing with the images they see and collect useful information*

<img src="https://raw.githubusercontent.com/JJGGtan/ICT_workshop2022/main/materials/pics/service_robot.png" width="500px">

*(Figure 6: An illustration of an intelligent mobile service robot
equipped with robot manipulator and computer vision [[4]](https://www.semanticscholar.org/paper/Comparisons-of-planar-detection-for-service-robot-Zhang-Huang/c1b02b251c68e8c3fd0ccdb16ad33f8769530afc))*

<u><i>[Real-time face mask detecting robot](https://smprobotics.com/usa/face-mask-detection-robot/)</u></i>

*This robot identifies if there are someones not wear a face mask in public and then it will alarm them to wear the mask with warning about the possibility of receiving a fine.*

<img src="https://smprobotics.com/wp-content/uploads/2020/11/robots_save_lives_during_a_pandemic.jpg" width="500px">

*(Figure credit: https://smprobotics.com/usa/face-mask-detection-robot/)*

<u><i>[People tracking mobile robot](https://m.unitree.com/products/a1)</u></i>

<img src="https://m.unitree.com/uploads/C0103_1_6_da055e532f.gif" width ="500px">

*(Figure credit: Unitree website https://m.unitree.com/products/a1)*

<u><i>Gripper controlling mini-project at REAI CMU</u></i>

<img src="https://raw.githubusercontent.com/JJGGtan/ICT_workshop2022/main/materials/pics/cmu_gripper.png" width="500px">

---

## ***References***

[1] Red Hat, Inc. “What Is an IDE?” Www.redhat.com, 8 Jan. 2019, www.redhat.com/en/topics/middleware/what-is-ide. Accessed 22 Aug. 2022.

[2] Baksheev, Kari; “Realtime Computer Vision with OpenCV.” Queue, vol. 10, no. 4, Apr. 2012, www.deepdyve.com/lp/association-for-computing-machinery/realtime-computer-vision-with-opencv-IFduHUOBOA, 10.1145/2181796.2206309. Accessed 22 Aug. 2022.

[3] Google LLC. “Mediapipe Hands”, https://google.github.io/mediapipe/solutions/hands. Accessed 22 Aug. 2022.

[4] Zhang, Zhijun et al. “Comparisons of planar detection for service robot with RANSAC and region growing algorithm.” 2017 36th Chinese Control Conference (CCC) (2017): 11092-11097.

[5] Maslov@made-In-Zelenograd.com, Maslov. “Face Mask Detection Robot with a Voice Warning of a Fine for Not Wearing It in the Public Area.” SMP Robotics - Autonomous Mobile Robot, SMP Robotics - Autonomous Mobile Robot, 20 Nov. 2020, https://smprobotics.com/usa/face-mask-detection-robot/. 

<img src="https://raw.githubusercontent.com/JJGGtan/ICT_workshop2022/main/materials/pics/wsend.png">
