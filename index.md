# BlueStamp Knee Rehab Device 
My project is a knee rehab device that monitors knee bending and warns users about excessive sudden movement during a bend. The system first checks if the knee is bent by at least 30° using the flex sensor. Once the bending threshold is reached, the IMU continuously measures the knee’s rotational speed. If the IMU detects a sudden rotation greater than the threshold, the movement is considered too fast or abrupt. When both conditions are met, the Arduino activates the buzzer and a red LED to immediately warn the user. This real-time feedback reminds the user to slow down and maintain proper, controlled movement during their rehab exercises. 


| **Engineer** | **School** | **Area of Interest** | **Grade** |
|:--:|:--:|:--:|:--:|
| Maggie Z | Lynbrook High | Electrical Engineering | Incoming Senior |

[here](https://tomcam.github.io/least-github-pages/adding-images-github-pages-site.html) 

![Headstone Image](logo.svg)
<img width="1040" height="533" alt="image" src="file:///Users/youjingzhang/Desktop/Screen%20Shot%202026-07-30%20at%201.54.12%20PM.png" />
  
# Final Milestone

**Don't forget to replace the text below with the embedding for your milestone video. Go to Youtube, click Share -> Embed, and copy and paste the code to replace what's below.**

<iframe width="560" height="315" src="https://www.youtube.com/embed/OUOKc4baLAE?si=yVW51Ad1745CydBu" title="My 3rd Milestone" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

Since my second milestone, I've soldered on on the components, transferring everything from my solder-less breadboard to the perf-board. I did the step before my imu calibration so that the readings wouldn't change afterward. The system first checks if the knee is bent by at least 30° using the flex sensor. Once the bending threshold is reached, the IMU continuously measures the knee’s rotational speed. If the IMU detects a sudden rotation greater than the threshold, the movement is considered too fast or abrupt. Right now, I have that threshold set to 0.5 rad/sec by default, but the user can adjust the value based on their rehab stage. 
My biggest challenge analyzing issues relating to my hardware components. After soldering the components, my device initially worked as expected, but one day it suddenly stopped functioning. Since the program had worked before, I knew the software was not the issue, so I concluded that the problem was likely related to the hardware. I replaced the USB cable, the adapter, and even the IMU, but the device still did not work. It wasn't until I replaced the microcontroller that the project finally started working again. Although the  process was long and frustrating, I was able to identify the faulty component and successfully resolve the issue.


<img src="image.jpg" alt="image" style="width: 100vw; height: auto;" src="https://github.com/user-attachments/assets/72220d5a-e1c6-4bda-a038-cd85c76940cd" />
Figure 2: function of accelerometer and gyroscope (https://www.circuitbread.com/ee-faq/how-do-accelerometers-and-gyroscopes-work)




# Second Milestone

**Don't forget to replace the text below with the embedding for your milestone video. Go to Youtube, click Share -> Embed, and copy and paste the code to replace what's below.**

<iframe width="560" height="315" src="https://www.youtube.com/embed/F-pjQPVt2HI?si=JOuxwe4WjZzyRa57" title="My 2nd Milestone" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

My second milestone consists of programming my bread board to read sensor data and activate the buzzer once the flex sensor is bent. The purpose of this is to detect when the knee is bending beyond a certain threshold and alert the user to maintain proper form during their exercises. 
In the function of my program, I set digital pin 9 on my Arduino as the buzzer's output and set analog pin 0 as an input to read values from my flex sensor. Basically, pin 9 creates the sound while pin 0 reads the bend value. The flex sensor changes value epending how much it is bent. When the felx sensor is straight, the value is higher, but once it's bent, the value decreases. The value represents the voltage, while the flex sensor acts as a resistor. When you bend the sensor, the resistance increases, so the voltage drops. The buzzer produces a sound once it's dropped beyond a certain value to alert the user of improper form. 
Challenges I've encoutered were mostly related to issues with my buzzer. Sometimes it would turn on after I bent my sensor, but it would continue even after the sensor returned to it's initial position. The Arduino froze after a delay, and it stopped updating the sensor readings. I had to remove code that stops the Arduino from running by deleting some delay commands. 
My program currently reads sensor data, but it doesn't detect incorrect movement using accelerometer. Basically, my code is checking whether the knee is bent and turns the buzzer on/off based on the sensor threshold. There's no logic that activates the buzzer if the movement is "incorrect"; examples of incorrect movement may include knees that wobble too much, tilting too far, unstability, etc. My next goal is for my program to detect incorrect movement. 


# First Milestone

**Don't forget to replace the text below with the embedding for your milestone video. Go to Youtube, click Share -> Embed, and copy and paste the code to replace what's below.**

<iframe width="932" height="524" src="https://www.youtube.com/embed/fE7zrK_g6vI" title="My 1st Milestone" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>


My knee rehab device is designed to help patients recover from knee injury. My goal is to construct a brace with sensors placed near the knee joint to measure bending angle and movement to track the user's progress. 
I've completed the hardware aspect of my project by completing the wiring for my breadboard. 
My knee device uses an Arduino Nano, the power source on my board; flex sensor, which detects knee bending; a buzzer, the signal to warn the user of improper form; and an accelerometer that measures the knee's movement. 
The Arduino nano recieves power from the USB cable and the voltage pin is connected to the power rail while the GND pin is connected to the ground rail. Since the Arduino cannot directly measure the resistance, the flex sensor is connected with a resistor of 10 kOhms to create a voltage divider. The flex sensor changes the resistance: when its straight there is a lower resistance, but the more it bends, the greater the resistance becomes. The Arduino recieves data of the movement and angle from the accelerometer, and they are connected through commuinications pins--SDA (serial data) and SCL (Serial Clock). If the knee bends too far, my arduino activates the buzzer that produces a warning. 
I've never used a flex sensor before the project, so it took me we while to understand how it actually works. I didn't realie that the sesnor acts as a resistor that changes value when you bend it. Once I understood its function, I realized that it couldn't be directly connected to the Arduino by itself. The Arduino can only read voltage, not resistance. I could finally wire my flex sensor on to the board correctly. One leg of my sensor is connected to 3.3 V (from my Arduino) and the other leg is connected to the ground rail of my board. 
My plan the complete my project is to program the board to read sensor data and activate the buzzer once the sensor is bent. Once I'm done with that, I can program my Arduino to detect incorrect movement, and then add any additional modifications to my project. 

<img width="715" height="279" alt="image" src="https://github.com/user-attachments/assets/025ccfe5-e094-4b78-b816-71146693427f" />

Figure 1: Diagram of flex sensor acting as a voltage divider (https://www.researchgate.net/figure/oltage-divider-circuit-for-flex-sensor-the-voltage-divider-circuit-is-connected-to-a_fig2_396461074)


# Schematics 
<img width="1040" height="533" alt="image" src="https://github.com/user-attachments/assets/78b97a0c-bf60-4dd9-b947-7befea6756b5" />
Diagram does not include the imu because the website that allowed me to develop the 3D model of my circuit did not include every electronic sensor component.

# Code

#include <Wire.h>
#include <Adafruit_LSM6DS3TRC.h>
#include <Adafruit_Sensor.h>

const int FLEX_PIN = A0;
const int BUTTON_PIN = 2;
const int BAD_FORM_LED_PIN = 6;      
const int BUZZER_PIN = 9;

// Flex sensor calibration values
const int FLEX_STRAIGHT = 760;
const int FLEX_BENT_90 = 700;

const float KNEE_BENT_ANGLE = 30.0;
const float ROTATION_LIMIT = 0.5;

Adafruit_LSM6DS3TRC lsm6ds;

float mapFloat(float value, float inMin, float inMax,
               float outMin, float outMax) {
  return (value - inMin) * (outMax - outMin) /
         (inMax - inMin) + outMin;
}

void setup() {
  Serial.begin(9600);
  Wire.begin();
  
  pinMode(FLEX_PIN, INPUT);
  
  pinMode(BUTTON_PIN, INPUT_PULLUP);
  
  pinMode(BAD_FORM_LED_PIN, OUTPUT);   

  pinMode(BUZZER_PIN, OUTPUT);

  digitalWrite(BAD_FORM_LED_PIN, LOW);

  noTone(BUZZER_PIN);

  Serial.println("Knee Rehab Device Started");

  if (!lsm6ds.begin_I2C()) {
    Serial.println("Failed to find LSM6DS3TR-C chip");

    while (true) {
      noTone(BUZZER_PIN):
      delay(10);
    }
  }

  lsm6ds.setAccelRange(LSM6DS_ACCEL_RANGE_2_G);
  lsm6ds.setAccelDataRate(LSM6DS_RATE_104_HZ);
  lsm6ds.setGyroRange(LSM6DS_GYRO_RANGE_250_DPS);
  lsm6ds.setGyroDataRate(LSM6DS_RATE_104_HZ);

  Serial.println("LSM6DS3TR-C found!");
  Serial.println("Accelerometer + gyroscope initialized");
}

void loop() {

  // Button LEDs
  bool buttonPressed = (digitalRead(BUTTON_PIN) == LOW);

  digitalWrite(LED_PRESSED_PIN, buttonPressed ? HIGH : LOW);
  digitalWrite(LED_NOT_PRESSED_PIN, buttonPressed ? LOW : HIGH);

  // Flex sensor
  int flexValue = analogRead(FLEX_PIN);

  float kneeAngle = mapFloat(
    flexValue,
    FLEX_STRAIGHT,
    FLEX_BENT_90,
    0.0,
    90.0
  );

  kneeAngle = constrain(kneeAngle, 0.0, 90.0);

  bool kneeBent = (kneeAngle >= KNEE_BENT_ANGLE);
// IMU
  sensors_event_t accel;
  sensors_event_t gyro;
  sensors_event_t temp;

  lsm6ds.getEvent(&accel, &gyro, &temp);

  float rotationAmount = sqrt(
    gyro.gyro.x * gyro.gyro.x +
    gyro.gyro.y * gyro.gyro.y +
    gyro.gyro.z * gyro.gyro.z
  );

  // Bad movement detection
  bool badForm = kneeBent && (rotationAmount > ROTATION_LIMIT);

  digitalWrite(BAD_FORM_LED_PIN, badForm ? HIGH : LOW);

  // Buzzer
  if (badForm) {
    tone(BUZZER_PIN, 1000);
  } else {
    noTone(BUZZER_PIN);
  }

  // Serial Monitor
  Serial.print("Flex: ");

  Serial.print(flexValue);

  Serial.print(" | Knee angle: ");
  Serial.print(kneeAngle, 1);

  Serial.print(" degrees | Rotation: ");
  Serial.print(rotationAmount, 3);

  Serial.print(" rad/s | ");

  if (badForm) {
    Serial.println("BAD FORM");
  } else if (kneeBent) {
    Serial.println("Knee bent - OK");
  } else {
    Serial.println("Knee straight");
  }

  delay(100);
}


# Bill of Materials
Here's where you'll list the parts in your project. To add more rows, just copy and paste the example rows below.
Don't forget to place the link of where to buy each component inside the quotation marks in the corresponding row after href =. Follow the guide [here]([url](https://www.markdownguide.org/extended-syntax/)) to learn how to customize this to your project needs. 

| **Part** | **Note** | **Price** | **Link** |
|:--:|:--:|:--:|:--:|
| Arduino Nano | Reads the voltage from the flex sensor and converts it into a value. The number tells the Arduino how much the knee bends. It reads the accelerometer to detect improper form and activates the buzzer to alert the user. In summary, it's the central controller that reads the sensors and activates the buzzer based on the movement into a value that tells us how far the knee bends and detect improper movement. | $18.30 | <a href="https://store-usa.arduino.cc/products/nano-esp32?utm_source=google&utm_medium=cpc&utm_campaign=US-Pmax&gad_source=4&gad_campaignid=21317508903&gbraid=0AAAAACbEa87jVwtKi6-0KAK5729eHSXbB&gclid=Cj0KCQjwg5zTBhCLARIsAP2AFU6rZtzJkZLsO7VXEeLA_S-Pb9Z-jM9AdwZK2Cpm-DuZn685pj2pn7AaAsOfEALw_wcB"> Link </a> |
| Flex sensor | Measures resistance and sends live data to the Arduino. The Arduino converts the resistance into a value that represents the bending angle | $8 | <a href="https://www.adafruit.com/product/1070?gad_source=1&gad_campaignid=23986111167&gbraid=0AAAAADx9JvRWfIagwA_odRNP7O4xBVBIs&gclid=Cj0KCQjwg5zTBhCLARIsAP2AFU6ZWOQXe508QTBXGOo9BbTlU8QujqZaJuU91L8yOV10IJeFKAnydLcaApFeEALw_wcB"> Link </a> |
| USB cable | upload program | $8 | <a href="google.com/aclk?sa=L&ai=DChsSEwja8a_dhPSVAxVaOkQIHX7OM4MYACICCAEQARoCZHo&co=1&ase=2&gclid=Cj0KCQjwg5zTBhCLARIsAP2AFU7xedcVY4HxarhOfi9muhvUJca_dCfK6pBriKk46MIVClkGUc0_IUAaAoZkEALw_wcB&cid=CAASugHkaIutptSxT2rXBK3hfHAngiZ6-HM2A3sToLwQFcxPn2IHqwocUR5Kol-B_FP2BQb_94IKGiA77skePiu75p880otF9gYrVd__VxLxqSWM_J_SCRCsRzT0HTfE8bEXRTHBvV69BBoqm6J5xWu0Qjr1yymegbcrpBBwxtDN9aVngxNkIrgvdZpMiSyXhu-RXqfPcDOfYLta0A4T5f_nOqAYmEk1FheafW-kEG2N6cjV6_uQZcyEzLA-7Vs&cce=2&category=acrcp_v1_32&sig=AOD64_2MMu5oPTjBR455ZVLxAd-AzckEfw&ctype=46&q&nis=4&adurl"> Link </a> |
| Jumper wires | Wire together electrical components | $3 | <a href="https://www.temu.com/ul/kuiper/un9.html?subj=goods-un&_bg_fs=1&_p_jump_id=894&_x_vst_scene=adg&goods_id=601103179287010&sku_id=17608427540400&adg_ctx=a-0cd7a592~c-5cd74d3a&_x_ads_sub_channel=shopping&_p_rfs=1&_x_ns_prz_type=-1&locale_override=211~en~USD&_x_ns_sku_id=17608427540400&_x_ns_gid=601103179287010&mrk_rec=1&_x_ads_channel=google&_x_gmc_account=647900107&_x_login_type=Google&_x_ns_gg_lnk_type=adr&_x_ads_account=1919904652&_x_ads_set=23243467838&_x_ads_id=188419728157&_x_ads_creative_id=783286123325&_x_ns_source=g&_x_ns_gclid=Cj0KCQjwg5zTBhCLARIsAP2AFU5vV7mQ1_b0vA6poCAJT6FBJlEATmenVyL0mfvsd0pLnYFj44C3xloaAm_OEALw_wcB&_x_ns_placement=&_x_ns_match_type=&_x_ns_ad_position=&_x_ns_product_id=17608427540400&_x_ns_target=&_x_ns_devicemodel=&_x_ns_wbraid=CkAKCAjw4JbTBhAoEjAAPV_IVxUl81qGYH_1ef0eUqPGjxOdrWacDgBJZBJZieO7M1kW4HPtnPGhAbutYCMaAqN8&_x_ns_gbraid=0AAAAAo4mICEc8OpyVpvisp-qQ159UVbI7&_x_ns_targetid=pla-2465604242337&gad_source=4&gad_campaignid=23243467838&gbraid=0AAAAAo4mICEc8OpyVpvisp-qQ159UVbI7&gclid=Cj0KCQjwg5zTBhCLARIsAP2AFU5vV7mQ1_b0vA6poCAJT6FBJlEATmenVyL0mfvsd0pLnYFj44C3xloaAm_OEALw_wcB"> Link </a> |
| Adafruit LSM6DS3TR-C IMU  | a motion sensor containing an accelerometer+gyroscope | $10 | <a href="https://www.adafruit.com/product/4503?gad_source=1&gad_campaignid=23986111167&gbraid=0AAAAADx9JvRWfIagwA_odRNP7O4xBVBIs&gclid=Cj0KCQjwg5zTBhCLARIsAP2AFU7nId49Vo06aj3CyZvp6ESHFaj_SeWtOTDrn0UbEQWn7ayjbu3wXwAaApe8EALw_wcB"> Link </a> |
| Piezo Buzzer | Acts as sound feedback to alert the user of improper form. After recieving a signal from an digital pun on my Arduino, it makes a tone. | $1.25 | <a href="https://www.amazon.com/Arduino-A000066-ARDUINO-UNO-R3/dp/B008GRTSV6/"> Link </a> |
| 100 ohm resistor  | protects buzzer by reducing current | $0.10 | <a href="https://www.jameco.com/z/AT-1438-TWT-R-JVP-Jameco-ValuePro-Magnetic-Buzzer-5V-4100-Hz-80dB-2-Pin_2337783.html?CID=GOOG&utm_source=google&utm_medium=ppc&utm_campaign=&utm_term=&utm_content=&gad_source=4&gad_campaignid=17336645193&gbraid=0AAAAADoyMrdc82OH5w__PgdIDOuIDUg-q&gclid=Cj0KCQjwg5zTBhCLARIsAP2AFU4PcgbFic3QGjgo02jFEQRaqu0-XmwmgiS1mpCkyaq8rl0xR-5KHSwaAinVEALw_wcB"> Link </a> |
| 10k ohm resistor  | Allows Arduino to detect "straight" vs "bent" knee before checking for improper form | $0.35 | <a href="https://www.jameco.com/z/RC0410K0JT-PC-Jameco-ValuePro-10k-Ohm-Resistor-5-1-4-Watt-Carbon-Film-Axial-POCO-Club-10-Pack-_2758575.html?srsltid=AfmBOooWQ7rejmOsQNYBuXlWUO88PlIQBvL7Vdd8H5qDITvDn4xXlmgN2g0"> Link </a> |
| perf-board | holds all my components | $3.5 | <a href="https://www.digikey.com/en/products/detail/digikey-standard/DKS-SOLDERBREAD-02/15970925?gclsrc=aw.ds&gad_source=4&gad_campaignid=20232005509&gbraid=0AAAAADrbLlioh5msBPNbwUGthunwz1tW4&gclid=Cj0KCQjwg5zTBhCLARIsAP2AFU7o3RxwU_7VCvHO7cR1VvjA13-8QQ1qXtOBlKdwqhIDTpOYXqrRlGkaAouTEALw_wcB)"> Link </a> |
| Knee sleeve | Acts as the foundation of my device; all the hardware aspects are attached to the knee sleeve.  | $8 | <a href="https://merabisisterhood.com/products/3d-knit-compression-knee-sleeve-breathable-multi-size-design?currency=USD&country=US&variant=53262966915339&stkn=3b915a1fb9f0&tw_source=google&tw_adid=&tw_campaign=24062156356&tw_kwdid=&gad_source=1&gad_campaignid=24052618788&gbraid=0AAAAA_zE7MvDcfAPxNfa6nmzBEoDBUsiq&gclid=Cj0KCQjwg5zTBhCLARIsAP2AFU795uTuUw3du6gswTWbgzl9nIedFesLVMu0KbAViY5Mi3dJeOPq-U0aAo9mEALw_wcB"> Link </a> |
| red LED | visual warning | $0.4 | <a href="https://www.homesciencetools.com/product/led-red-diffuse-type-5-mm/?tw_source=google&tw_adid=&tw_campaign=22803833960&tw_kwdid=&gad_source=1&gad_campaignid=22798006302&gbraid=0AAAAAD_l2qlRDYrq9yad0OuikOc5h4fIS&gclid=Cj0KCQjwg5zTBhCLARIsAP2AFU4nPqUvALRF1-hyZ_vabixKE1PsbH_SdcivWzQ89YJ2R3VcOBV8uQgaAkueEALw_wcB"> Link </a> |


# Other Resources/Examples
- [Student Portfolio](https://samvratgowda.github.io/Samvrat-Gowda-BSE-Portfolio/)
- [Shrink tubing tutorial](https://www.youtube.com/watch?v=VgnHuJGocZI)
- [Arduino pins](https://docs.arduino.cc/learn/microcontrollers/digital-pins//)

