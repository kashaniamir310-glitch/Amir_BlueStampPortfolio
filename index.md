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


Modification Schematic:



<div style="
  height: 350px;
  overflow-y: auto;
  overflow-x: hidden;
  background-color: #1e1e1e;
  color: white;
  padding: 15px;
  border-radius: 8px;
">
  <pre style="
    margin: 0;
    white-space: pre-wrap;
    overflow-wrap: anywhere;
    word-break: break-word;
    font-family: Consolas, monospace;
    font-size: 14px;
    line-height: 1.5;
  "><code>

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

  </code></pre>
</div>


# Bill of Materials

| **Part** | **Note** | **Price** | **Link** |
|:--:|:--:|:--:|:--:|
| LK COKOINO Robot Arm for Arduino Kit | Contains most of the electronics and structural parts to effectively build the robot arm like the servos | 67.59 USD | <a href="https://www.ebay.com/itm/198408400389?_trkparms=itmf%3D1%26aid%3D1110006%26rkt%3D5%26pid%3D101224%26mech%3D1%26algv%3DSimOrganicCassiniWithToraRecalls%26pmt%3D1%26amclksrc%3DITM%26sd%3D157474275192%26sid%3DAQALAAAAEGBkDzBJog7ypwIqS4R9%2Fyc%3D%26itm%3D198408400389%26noa%3D1%26plcampt%3D0%3A156209825015%26algo%3DHOMESPLICE.SIM%26brand%3DArduino%26asc%3D20200818143230%26ao%3D1%26rk%3D1%26mehot%3Dnone%26lsid%3D0%26meid%3D45a14a6229e74a4287ac2b1e6d9a37f0%26pg%3D2332490&_trksid=p2332490.c101224.m-1"> eBay </a> |
| 8-Pack 9V Long-Lasting Alkaline Batteries | Powering the robot arm with voltage | 12.69 USD | <a href="https://www.amazon.com/Amazon-Basics-Performance-All-Purpose-Batteries/dp/B00MH4QM1S?th=1"> Amazon </a> |
| 9V Barrel Jack/Battery Clip | Connects the 9V Alkaline Batteries to be connected to the Nano | 6.99 USD | <a href="https://www.amazon.com/Chanzon-Battery-2-1x5-5mm-Connector-Leather/dp/B083QFNY1G/ref=sr_1_2_sspa?dib=eyJ2IjoiMSJ9.FGP7Lz9l0Lv576xrynIBqFWeMc3LXOk3pb7inRGVIxuKFx-qMixlo9HwVRm5NM_qRau1H7rjns8U2pd7R-JWV1E_ZsOi4LPIOTi2lAwDlTdvZiwnUucxOPb6OD345YH1z31I1s0nxmhkpos-pMYPx1Ava_N1fIFjcHhkSyIHm4y_PCE0erY-vh4FBT216vIvy1ylQChhGLTv8_ReSW_ALbSLagl98P4Hi2-QGZkZmiE.xVlxQO58o51J75GF_xTLx3tQriagnpKYQ9JvgtKfm-Y&dib_tag=se&keywords=9v%2Bjack&qid=1786120595&sr=8-2-spons&sp_csd=d2lkZ2V0TmFtZT1zcF9hdGY&th=1"> Amazon </a> |
| Smraza Electronics Components Kit for Arduino | Provides lots of handy electronic components like jumper wires, buttons, LEDs, etc. | 14.99 USD | <a href="https://www.amazon.com/Smraza-Electronics-Potentiometer-tie-Points-Breadboard/dp/B0B62RL725/ref=sxts_b2b_sx_reorder_acb_business?content-id=amzn1.sym.f63a3b0b-3a29-4a8e-8430-073528fe007f%3Aamzn1.sym.f63a3b0b-3a29-4a8e-8430-073528fe007f&crid=2IC3T44H3U3WG&cv_ct_cx=breadboard%2Bkit&dib=eyJ2IjoiMSJ9.TUd5tu2T8rmms7ZuJ0UzmbtpLL1zsu93bQM0PzwnP4E.sT0V0vL_QtbYv8ymVTCcRkhFNgBtRvRiT7G4FT1oGTE&dib_tag=se&keywords=breadboard%2Bkit&pd_rd_i=B0B62RL725&pd_rd_r=67e1f4ff-e3b9-44e4-b441-b4ae282f036b&pd_rd_w=UjFaP&pd_rd_wg=0xRoC&pf_rd_p=f63a3b0b-3a29-4a8e-8430-073528fe007f&pf_rd_r=BFGP77H27ZN31W4PZAW6&qid=1715911733&sbo=RZvfv%2F%2FHxDF%2BO5021pAnSA%3D%3D&sprefix=breadboard%2Bkit%2Caps%2C109&sr=1-2-9f062ed5-8905-4cb9-ad7c-6ce62808241a&th=1"> Amazon </a> |
| Arduino Nano Expansion Shield | Allows Arduino Nano to be connected to many different things like servos without the use of a breadboard | 0.99 USD | <a href="https://www.aliexpress.us/item/3256806789828336.html?src=google&src=google&albch=shopping&acnt=708-803-3821&isdl=y&slnk=&plac=&mtctp=&albbt=Google_7_shopping&aff_platform=google&aff_short_key=UneMJZVf&gclsrc=aw.ds&albagn=888888&ds_e_adid=&ds_e_matchtype=&ds_e_device=c&ds_e_network=x&ds_e_product_group_id=&ds_e_product_id=en3256806789828336&ds_e_product_merchant_id=5308071469&ds_e_product_country=US&ds_e_product_language=en&ds_e_product_channel=online&ds_e_product_store_id=&ds_url_v=2&albcp=19558607238&albag=&isSmbAutoCall=false&needSmbHouyi=false&gad_source=1&gad_campaignid=19566915268&gclid=CjwKCAjwhNbTBhB4EiwAsFSg-hFQWGG4r5jQceGYKZGmwf6L-8Qp2mKNq5GyotZmTgca1PBfgzyhNRoChrIQAvD_BwE&gatewayAdapt=glo2usa"> AliExpress </a> |
| Digital Multimeter | Used to measure the strength of electric current | 30.29 USD | <a href="https://www.ebay.com/itm/374967738363?chn=ps&mkevt=1&mkcid=28&google_free_listing_action=view_item&srsltid=AfmBOopnn0ydYP5kXymJipweZaCJ0vsFqzgmlKVPesQbOBNPAaOiL_lVR00&com_cvv=8fb3d522dc163aeadb66e08cd7450cbbdddc64c6cf2e8891f6d48747c6d56d2c"> eBay </a> |
| 32 In 1 Small Screwdriver Set | Multi-head screwdriver kit allowing me to screw in any screw regardless of size | 7.99 USD | <a href="https://www.amazon.com/Small-Screwdriver-Set-Mini-Magnetic/dp/B08RYXKJW9"> Amazon </a> |


# Other Resources/Examples

- [Example 1](https://trashytuber.github.io/YimingJiaBlueStamp/)
- [Example 2](https://sviatil0.github.io/Sviatoslav_BSE/)
- [Example 3](https://arneshkumar.github.io/arneshbluestamp/)

