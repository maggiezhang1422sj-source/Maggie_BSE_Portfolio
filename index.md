# BlueStamp Knee Rehab Device 
Replace this text with a brief description (2-3 sentences) of your project. This description should draw the reader in and make them interested in what you've built. You can include what the biggest challenges, takeaways, and triumphs from completing the project were. As you complete your portfolio, remember your audience is less familiar than you are with all that your project entails!

You should comment out all portions of your portfolio that you have not completed yet, as well as any instructions:
```HTML 
<!--- This is an HTML comment in Markdown -->
<!--- Anything between these symbols will not render on the published site -->
```

| **Engineer** | **School** | **Area of Interest** | **Grade** |
|:--:|:--:|:--:|:--:|
| Maggie Z | Lynbrook High | Electrical Engineering | Incoming Senior |

**Replace the BlueStamp logo below with an image of yourself and your completed project. Follow the guide [here](https://tomcam.github.io/least-github-pages/adding-images-github-pages-site.html) if you need help.**

![Headstone Image](logo.svg)
  
# Final Milestone

**Don't forget to replace the text below with the embedding for your milestone video. Go to Youtube, click Share -> Embed, and copy and paste the code to replace what's below.**

<iframe width="560" height="315" src="https://www.youtube.com/embed/F7M7imOVGug" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

For your final milestone, explain the outcome of your project. Key details to include are:
- What you've accomplished since your previous milestone
- What your biggest challenges and triumphs were at BSE
- A summary of key topics you learned about
- What you hope to learn in the future after everything you've learned at BSE





# Second Milestone

**Don't forget to replace the text below with the embedding for your milestone video. Go to Youtube, click Share -> Embed, and copy and paste the code to replace what's below.**

<iframe width="560" height="315" src="https://www.youtube.com/watch?v=F-pjQPVt2HI" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

My second milestone consists of programming my bread board to read sensor data and activate the buzzer once the flex sensor is bent. The purpose of this is to detect when the knee is bending beyond a certain threshold and alert the user to maintain proper form during their exercises. 
In the function of my program, I set digital pin 9 on my Arduino as the buzzer's output and set analog pin 0 as an input to read values from my flex sensor. Basically, pin 9 creates the sound while pin 0 reads the bend value. The flex sensor changes value epending how much it is bent. When the felx sensor is straight, the value is higher, but once it's bent, the value decreases. The value represents the voltage, while the flex sensor acts as a resistor. When you bend the sensor, the resistance increases, so the voltage drops. The buzzer produces a sound once it's dropped beyond a certain value to alert the user of improper form. 
Challenges I've encoutered were mostly related to issues with my buzzer. Sometimes it would turn on after I bent my sensor, but it would continue even after the sensor returned to it's initial position. The Arduino froze after a delay, and it stopped updating the sensor readings. I had to remove code that stops the Arduino from running by deleting some delay commands. 
My program currently reads sensor data, but it doesn't detect incorrect movement using accelerometer. Basically, my code is checking whether the knee is bent and turns the buzzer on/off based on the sensor threshold. There's no logic that activates the buzzer if the movement is "incorrect"; examples of incorrect movement may include knees that wobble too much, tilting too far, unstability, etc. My next goal is for my program to detect incorrect movement. 


# First Milestone

**Don't forget to replace the text below with the embedding for your milestone video. Go to Youtube, click Share -> Embed, and copy and paste the code to replace what's below.**

<iframe width="932" height="524" src="https://www.youtube.com/embed/fE7zrK_g6vI" title="Maggie Z. Milestone 1" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>


My knee rehab device is designed to help patients recover from knee injury. My goal is to construct a brace with sensors placed near the knee joint to measure bending angle and movement to track the user's progress. 
I've completed the hardware aspect of my project by completing the wiring for my breadboard. 
My knee device uses an Arduino Nano, the power source on my board; flex sensor, which detects knee bending; a buzzer, the signal to warn the user of improper form; and an accelerometer that measures the knee's movement. 
The Arduino nano recieves power from the USB cable and the voltage pin is connected to the power rail while the GND pin is connected to the ground rail. Since the Arduino cannot directly measure the resistance, the flex sensor is connected with a resistor of 10 kOhms to create a voltage divider. The flex sensor changes the resistance: when its straight there is a lower resistance, but the more it bends, the greater the resistance becomes. The Arduino recieves data of the movement and angle from the accelerometer, and they are connected through commuinications pins--SDA (serial data) and SCL (Serial Clock). If the knee bends too far, my arduino activates the buzzer that produces a warning. 
I've never used a flex sensor before the project, so it took me we while to understand how it actually works. I didn't realie that the sesnor acts as a resistor that changes value when you bend it. Once I understood its function, I realized that it couldn't be directly connected to the Arduino by itself. The Arduino can only read voltage, not resistance. I could finally wire my flex sensor on to the board correctly. One leg of my sensor is connected to 3.3 V (from my Arduino) and the other leg is connected to the ground rail of my board. 
My plan the complete my project is to program the board to read sensor data and activate the buzzer once the sensor is bent. Once I'm done with that, I can program my Arduino to detect incorrect movement, and then add any additional modifications to my project. 

# Schematics 
Here's where you'll put images of your schematics. [Tinkercad](https://www.tinkercad.com/blog/official-guide-to-tinkercad-circuits) and [Fritzing](https://fritzing.org/learning/) are both great resoruces to create professional schematic diagrams, though BSE recommends Tinkercad becuase it can be done easily and for free in the browser. 
<img width="1040" height="533" alt="image" src="https://github.com/user-attachments/assets/78b97a0c-bf60-4dd9-b947-7befea6756b5" />


# Code
Here's where you'll put your code. The syntax below places it into a block of code. Follow the guide [here]([url](https://www.markdownguide.org/extended-syntax/)) to learn how to customize it to your project needs. 

#include <Wire.h>
#include <Adafruit_LSM6DS3TRC.h>


const int FLEX_PIN = A0;
const int BUTTON_PIN = 2;
const int LED_PRESSED_PIN = 4;
const int LED_NOT_PRESSED_PIN = 7;
const int BUZZER_PIN = 9;

//flex sensor 
const int FLEX_STRAIGHT = 760;  // approximately 0 degrees
const int FLEX_BENT_90 = 700;   // approximately 90 degrees

const float KNEE_BENT_ANGLE = 30.0;        // begin checking form after this bend
const float ROTATION_LIMIT = 0.5;          // radians/second; adjust after testing

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
  pinMode(LED_PRESSED_PIN, OUTPUT);
  pinMode(LED_NOT_PRESSED_PIN, OUTPUT);
  pinMode(BUZZER_PIN, OUTPUT);

  noTone(BUZZER_PIN);

  Serial.println("Knee Rehab Device Started");

  if (!lsm6ds.begin_I2C()) {
    Serial.println("Failed to find LSM6DS3TR-C chip");
    while (true) {
      noTone(BUZZER_PIN);
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
  // LED
  bool buttonPressed = (digitalRead(BUTTON_PIN) == LOW);

  digitalWrite(LED_PRESSED_PIN, buttonPressed ? HIGH : LOW);
  digitalWrite(LED_NOT_PRESSED_PIN, buttonPressed ? LOW : HIGH);

  //flex sensor+knee angle
  int flexValue = analogRead(FLEX_PIN);

  float kneeAngle = mapFloat(
    flexValue,
    FLEX_STRAIGHT, FLEX_BENT_90,
    0.0, 90.0
  );

  kneeAngle = constrain(kneeAngle, 0.0, 90.0);
  bool kneeBent = (kneeAngle >= KNEE_BENT_ANGLE);

  // imu 
  sensors_event_t accel;
  sensors_event_t gyro;
  sensors_event_t temp;

  lsm6ds.getEvent(&accel, &gyro, &temp);

  float rotationAmount = sqrt(
    gyro.gyro.x * gyro.gyro.x +
    gyro.gyro.y * gyro.gyro.y +
    gyro.gyro.z * gyro.gyro.z
  );

  // Bad form = rotating too quickly while knee is bent.
  bool badForm = kneeBent && (rotationAmount > ROTATION_LIMIT);

  // buzzer activation
  if (badForm) {
    tone(BUZZER_PIN, 1000);
  } else {
    noTone(BUZZER_PIN);
  }

  // printed on serial moniter 
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
| Arduino Nano | Reads the voltage from the flex sensor and converts it into a value. The number tells the Arduino how much the knee bends. It reads the accelerometer to detect improper form and activates the buzzer to alert the user. In summary, it's the central controller that reads the sensors and activates the buzzer based on the movement into a value that tells us how far the knee bends and detect improper movement. | $20-25 | <a href="https://www.amazon.com/Arduino-A000066-ARDUINO-UNO-R3/dp/B008GRTSV6/"> Link </a> |
| Flex sensor | Measures resistance and sends live data to the Arduino. The Arduino converts the resistance  | $8 | <a href="https://www.amazon.com/Arduino-A000066-ARDUINO-UNO-R3/dp/B008GRTSV6/"> Link </a> |
| USB cable | What the item is used for | $10 | <a href="https://www.amazon.com/Arduino-A000066-ARDUINO-UNO-R3/dp/B008GRTSV6/"> Link </a> |
| Jumper wires | What the item is used for | $7 | <a href="https://www.amazon.com/Arduino-A000066-ARDUINO-UNO-R3/dp/B008GRTSV6/"> Link </a> |
| Accelerometer | What the item is used for | $20 | <a href="https://www.amazon.com/Arduino-A000066-ARDUINO-UNO-R3/dp/B008GRTSV6/"> Link </a> |
| Piezo Buzzer | Acts as sound feedback to alert the user of improper form. After recieving a signal from an digital pun on my Arduino, it makes a tone. | $3 | <a href="https://www.amazon.com/Arduino-A000066-ARDUINO-UNO-R3/dp/B008GRTSV6/"> Link </a> |
| 100 ohm resistor  | What the item is used for | $0.10 | <a href="https://www.amazon.com/Arduino-A000066-ARDUINO-UNO-R3/dp/B008GRTSV6/"> Link </a> |
| 10 kohm resistor  | What the item is used for | $0.06 | <a href="https://www.amazon.com/Arduino-A000066-ARDUINO-UNO-R3/dp/B008GRTSV6/"> Link </a> |
| Breadboard | What the item is used for | $2.5` | <a href="https://www.amazon.com/Arduino-A000066-ARDUINO-UNO-R3/dp/B008GRTSV6/"> Link </a> |
| Knee sleeve | Acts as thr foundation of my device; all the hardware aspects are attached to the knee sleeve.  | $Price | <a href="https://www.amazon.com/Arduino-A000066-ARDUINO-UNO-R3/dp/B008GRTSV6/"> Link </a> |


# Other Resources/Examples
One of the best parts about Github is that you can view how other people set up their own work. Here are some past BSE portfolios that are awesome examples. You can view how they set up their portfolio, and you can view their index.md files to understand how they implemented different portfolio components.
- [Example 1](https://trashytuber.github.io/YimingJiaBlueStamp/)
- [Example 2](https://sviatil0.github.io/Sviatoslav_BSE/)
- [Example 3](https://arneshkumar.github.io/arneshbluestamp/)

To watch the BSE tutorial on how to create a portfolio, click here.
