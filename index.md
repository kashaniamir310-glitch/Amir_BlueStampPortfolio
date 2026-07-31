# Three-Jointed Robotic Arm

For this project, I built and programmed a three-jointed robotic arm using an Arduino Nano, four servo motors, and a dual joystick module. Throughout the project, I experienced both successes and challenges that helped strengthen my engineering and problem solving skills. One of my biggest accomplishments was finally tightening the last screw of the robot and preparing to debug the system and add modifications. One challenge I encountered was a jittery gripper caused by a short circuit. After troubleshooting the issue, I discovered that the copper standoffs supporting the Arduino were touching the soldered pins underneath the board. I resolved the problem by removing all but one of the copper standoffs, which prevented unwanted electrical contact and restored smooth operation. Overall, this project was a valuable and enjoyable experience that improved my understanding of electronics, programming, and mechanical assembly.

| **Engineer** | **School** | **Area of Interest** | **Grade** |
|:--:|:--:|:--:|:--:|
| Amir Kashani | Rochester Mayo High School | Biomedical Engineering | Incoming Freshman

<img width="660" height="480" alt="IMG_1124" src="https://github.com/user-attachments/assets/6662adcb-753d-42bb-aaf3-503bb3e64980" />

  
# Final Milestone

**Don't forget to replace the text below with the embedding for your milestone video. Go to Youtube, click Share -> Embed, and copy and paste the code to replace what's below.**

<iframe width="560" height="315" src="https://www.youtube.com/embed/F7M7imOVGug" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

For your final milestone, explain the outcome of your project. Key details to include are:
- What you've accomplished since your previous milestone
- What your biggest challenges and triumphs were at BSE
- A summary of key topics you learned about
- What you hope to learn in the future after everything you've learned at BSE

# First Milestone

<iframe width="560" height="315" src="https://www.youtube.com/embed/RoVlW-vudJY?si=_0385IkFJLN00zUr" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>


For my first milestone in the BlueStamp Engineering Remote Program, I completed the base version of my Arduino robotic arm. This milestone focused on assembling the hardware, wiring all of the electronic components, and developing the software needed to control the arm.

The robot consists of four servo motors that provide movement at the  base, shoulder, elbow, and gripper joints. Each servo is controlled using two joystick modules, allowing the arm to move smoothly in real time. The joystick modules output analog voltage signals that the Arduino reads through its analog input pins. The Arduino then converts these values into servo angles, enabling intuitive manual control of each joint.

One of the biggest challenges during this milestone was eliminating jittering and the unreponsive control of the servo that flexed and extended the gripper. This occured due to the short-circuiting of the Nano Shield that was connected to my microcontroller. In order to fix it, I removed all but one of the copper pillars that were touching the soldered pins under the shield. 

With the base project now complete, my future milestones will focus on improving the robotic arm's capabilities by customizing the code the induce different motor functions, replacing the various weak servos, and providing the robot with a compact and accesible enclosure built for functionality. This milestone establishes a solid hardware and software foundation for the rest of the project.

# Schematics 

Base Project Schematic:

<img width="630" height="667" alt="image" src="https://github.com/user-attachments/assets/38c5763a-7fbd-4b18-a5b7-0a6772251e88" />


# Code

```c++
#include "src/CokoinoArm.h"

#define buzzerPin 9



CokoinoArm arm;

int xL,yL,xR,yR;



const int act_max=10;    //Default 10 action,4 the Angle of servo

int act[act_max][4];    //Only can change the number of action

int num=0,num_do=0;

///////////////////////////////////////////////////////////////

void turnUD(void){

  if(xL!=512){

    if(0<=xL && xL<=100){arm.up(10);return;}

    if(900<xL && xL<=1024){arm.down(10);return;} 

    if(100<xL && xL<=200){arm.up(20);return;}

    if(800<xL && xL<=900){arm.down(20);return;}

    if(200<xL && xL<=300){arm.up(25);return;}

    if(700<xL && xL<=800){arm.down(25);return;}

    if(300<xL && xL<=400){arm.up(30);return;}

    if(600<xL && xL<=700){arm.down(30);return;}

    if(400<xL && xL<=480){arm.up(35);return;}

    if(540<xL && xL<=600){arm.down(35);return;} 

    }

}

///////////////////////////////////////////////////////////////

void turnLR(void){

  if(yL!=512){

    if(0<=yL && yL<=100){arm.right(0);return;}

    if(900<yL && yL<=1024){arm.left(0);return;}  

    if(100<yL && yL<=200){arm.right(5);return;}

    if(800<yL && yL<=900){arm.left(5);return;}

    if(200<yL && yL<=300){arm.right(10);return;}

    if(700<yL && yL<=800){arm.left(10);return;}

    if(300<yL && yL<=400){arm.right(15);return;}

    if(600<yL && yL<=700){arm.left(15);return;}

    if(400<yL && yL<=480){arm.right(20);return;}

    if(540<yL && yL<=600){arm.left(20);return;}

  }

}

///////////////////////////////////////////////////////////////

void turnCO(void){

  if(xR!=512){

    if(0<=xR && xR<=100){arm.close(0);return;}

    if(900<xR && xR<=1024){arm.open(0);return;} 

    if(100<xR && xR<=200){arm.close(5);return;}

    if(800<xR && xR<=900){arm.open(5);return;}

    if(200<xR && xR<=300){arm.close(10);return;}

    if(700<xR && xR<=800){arm.open(10);return;}

    if(300<xR && xR<=400){arm.close(15);return;}

    if(600<xR && xR<=700){arm.open(15);return;}

    if(400<xR && xR<=480){arm.close(20);return;}

    if(540<xR && xR<=600){arm.open(20);return;} 

    }

}

///////////////////////////////////////////////////////////////

void date_processing(int *x,int *y){

  if(abs(512-*x)>abs(512-*y))

    {*y = 512;}

  else

    {*x = 512;}

}

///////////////////////////////////////////////////////////////

void buzzer(int H,int L){

  while(yR<420){

    digitalWrite(buzzerPin,HIGH);

    delayMicroseconds(H);

    digitalWrite(buzzerPin,LOW);

    delayMicroseconds(L);

    yR = arm.JoyStickR.read_y();

    }

  while(yR>600){

    digitalWrite(buzzerPin,HIGH);

    delayMicroseconds(H);

    digitalWrite(buzzerPin,LOW);

    delayMicroseconds(L);

    yR = arm.JoyStickR.read_y();

    }

}

///////////////////////////////////////////////////////////////

void C_action(void){

  if(yR>800){

    int *p;

    p=arm.captureAction();

    for(char i=0;i<4;i++){

    act[num][i]=*p;

    p=p+1;     

    }

    num++;

    num_do=num;

    if(num>=act_max){

      num=0;

      buzzer(600,400);

      }

    while(yR>600){yR = arm.JoyStickR.read_y();}

    //Serial.println(act[0][0]);

  }

}

///////////////////////////////////////////////////////////////

void Do_action(void){

  if(yR<220){

    buzzer(200,300);

    for(int i=0;i<num_do;i++){

      arm.do_action(act[i],15);

      }

    num=0;

    while(yR<420){yR = arm.JoyStickR.read_y();}

    for(int i=0;i<2000;i++){

      digitalWrite(buzzerPin,HIGH);

      delayMicroseconds(200);

      digitalWrite(buzzerPin,LOW);

      delayMicroseconds(300);        

    }

  }

}

///////////////////////////////////////////////////////////////

void setup() {

  //Serial.begin(9600);

  //arm of servo motor connection pins

  arm.ServoAttach(4,5,6,7);

  //arm of joy stick connection pins : xL,yL,xR,yR

  arm.JoyStickAttach(A0,A1,A2,A3);

  pinMode(buzzerPin,OUTPUT);

}

///////////////////////////////////////////////////////////////

void loop() {

  xL = arm.JoyStickL.read_x();

  yL = arm.JoyStickL.read_y();

  xR = arm.JoyStickR.read_x();

  yR = arm.JoyStickR.read_y();

  date_processing(&xL,&yL);

  date_processing(&xR,&yR);

  turnUD();

  turnLR();

  turnCO();

  C_action();

  Do_action();

}   

```

# Bill of Materials

| **Part** | **Note** | **Price** | **Link** |
|:--:|:--:|:--:|:--:|
| LK COKOINO Robot Arm for Arduino Kit | Contains most of the electronics and structural parts to effectively build the robot arm | 67.59 USD | <a href="https://www.ebay.com/itm/198408400389?_trkparms=itmf%3D1%26aid%3D1110006%26rkt%3D5%26pid%3D101224%26mech%3D1%26algv%3DSimOrganicCassiniWithToraRecalls%26pmt%3D1%26amclksrc%3DITM%26sd%3D157474275192%26sid%3DAQALAAAAEGBkDzBJog7ypwIqS4R9%2Fyc%3D%26itm%3D198408400389%26noa%3D1%26plcampt%3D0%3A156209825015%26algo%3DHOMESPLICE.SIM%26brand%3DArduino%26asc%3D20200818143230%26ao%3D1%26rk%3D1%26mehot%3Dnone%26lsid%3D0%26meid%3D45a14a6229e74a4287ac2b1e6d9a37f0%26pg%3D2332490&_trksid=p2332490.c101224.m-1"> eBay </a> |
| 8-Pack 9V Long-Lasting Alkaline Batteries | Powering the robot arm with voltage | 12.69 USD | <a href="https://www.amazon.com/Amazon-Basics-Performance-All-Purpose-Batteries/dp/B00MH4QM1S?th=1"> Amazon </a> |
| Item Name | What the item is used for | $Price | <a href=""> Link </a> |

# Other Resources/Examples

- [Example 1](https://trashytuber.github.io/YimingJiaBlueStamp/)
- [Example 2](https://sviatil0.github.io/Sviatoslav_BSE/)
- [Example 3](https://arneshkumar.github.io/arneshbluestamp/)

