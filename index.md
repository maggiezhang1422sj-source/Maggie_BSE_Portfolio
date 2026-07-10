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

<iframe width="560" height="315" src="https://www.youtube.com/embed/y3VAmNlER5Y" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

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

# Code
Here's where you'll put your code. The syntax below places it into a block of code. Follow the guide [here]([url](https://www.markdownguide.org/extended-syntax/)) to learn how to customize it to your project needs. 

#include <Adafruit_LSM6DS3TRC.h>
#include <Adafruit_LIS3MDL.h>


Adafruit_LIS3MDL lis3mdl;
Adafruit_LSM6DS3TRC lsm6ds;


int int_timer = 0;

int accelX = 0;

int accelY = 0;

int accelZ = 0;

int gyroX = 0;

int gyroY = 0;

int gyroZ = 0;

int temp = 0;

int sensorValue = 0;

int buttonState = 0;

void setup()
{
  pinMode(9, OUTPUT); //sets pin 9 -> buzzer
  Serial.begin(9600);
  pinMode(4, OUTPUT); 
  pinMode(7, OUTPUT);
  //sets pin 4 & 7 -> LEDs
  pinMode(A0, INPUT); //sets A0-> flex sensor input
  pinMode(9, OUTPUT);

  digitalWrite(9, LOW);
  Serial.println("Knee Rehab Device started");

  //accelerometer set up (from somewhere online to check if the accelerometer is working):
  //modify it eventually
  if (!lsm6ds.begin_I2C()) { //check if sensor connected 
    Serial.println("Failed to find LSM6DS3TR-C chip"); //sensor didn't initialize 
    while (1) delay(10); // stop program
  }
  Serial.println("LSM6DS3TR-C found!"); //sesnor works 

  // Configure accelerometer
  lsm6ds.setAccelRange(LSM6DS_ACCEL_RANGE_2_G); //meausres acceleration in terms of gravity; set to 2G
  lsm6ds.setAccelDataRate(LSM6DS_RATE_104_HZ); //104 readings/sec

  // Configure gyroscope
  lsm6ds.setGyroRange(LSM6DS_GYRO_RANGE_250_DPS); //can detect rotation up to +-250°/sec 
  lsm6ds.setGyroDataRate(LSM6DS_RATE_104_HZ); //104 readings/sec

  

  Serial.println("Accelerometer + Gyro initialized");
  

  

  
}

void loop()
{
  buttonState = digitalRead(2);
  if (buttonState == LOW) {
    digitalWrite(4, HIGH);
    //since buttonState is always 0, if condition always true
    delay(100); // Wait for 100 millisecond(s)
    digitalWrite(4, LOW);
    delay(100); // Wait for 100 millisecond(s)
  } else {
    digitalWrite(7, HIGH);
    delay(100); // Wait for 100 millisecond(s)
  } 

  sensorValue = analogRead(A0); //reads flex sensor; pin no is the arguement 
  Serial.println(sensorValue); //prints voltage values 
  //float Vflex = sensorValue * 3.3 / 1023.0;  
  //float Rflex = 10000.0 * (3.3 / Vflex - 1.0);  
  //float angle = map(Rflex, 25000.0, 100000.0, 0, 90);
  //angle = constrain(angle, 0, 90);
  if (sensorValue < 850) {
    tone(9, 5274); // play tone 100 (E8 = 5274 Hz)
    //turn buzzer on if bent
    //digitalWrite(9, HIGH);
    Serial.println("hi"); //remeber to delete this line 
    
  } else {
    noTone(9);
    Serial.println("bye"); //remeber to delete this line
    
  }
  //turn buzzer off
  delay(10); // Wait for 10 millisecond(s)

  //read motion data (acceleration+rotation) from LSM6DS3TR‑C
  sensors_event_t accel;
  sensors_event_t gyro;
  sensors_event_t tempEvent;


  lsm6ds.getEvent(&accel, &gyro, &tempEvent); //reads sensor data
  //&tempEven not necassary, but Adafruit_LSM6DS3TRC library requires three arguments in getEvent()

  float accelX = accel.acceleration.x; //forward/backward lean
  float accelY = accel.acceleration.y; //left/right lean
  float accelZ = accel.acceleration.z; //vertical acceleration 

  //helps detect wobbling or rotational instability 
  float gyroX = gyro.gyro.x; //forward/backward rotation
  float gyroY = gyro.gyro.y; //left/right rotation
  float gyroZ = gyro.gyro.z; //vertical rotation


  //prints data to serial moniter 
  Serial.print("Accel X: "); Serial.print(accelX);
  Serial.print("  Y: "); Serial.print(accelY);
  Serial.print("  Z: "); Serial.println(accelZ);

  Serial.print("Gyro X: "); Serial.print(gyroX);
  Serial.print("  Y: "); Serial.print(gyroY);
  Serial.print("  Z: "); Serial.println(gyroZ);


}

//Rflex = ((3.3/A0)-1)*10k
//Vcc= 3.3, R_DIV=10k



# Bill of Materials
Here's where you'll list the parts in your project. To add more rows, just copy and paste the example rows below.
Don't forget to place the link of where to buy each component inside the quotation marks in the corresponding row after href =. Follow the guide [here]([url](https://www.markdownguide.org/extended-syntax/)) to learn how to customize this to your project needs. 

| **Part** | **Note** | **Price** | **Link** |
|:--:|:--:|:--:|:--:|
| Arduino Nano | Reads the voltage from the flex sensor and converts it into a value. The number tells the Arduino how much the knee bends. It reads the accelerometer to detect improper form and activates the buzzer to alert the user. In summary, it's the central controller that reads the sensors and activates the buzzer based on the movement  | $20-25 | <a href="https://www.amazon.com/Arduino-A000066-ARDUINO-UNO-R3/dp/B008GRTSV6/"> Link </a> |
| Flex sensor | What the item is used for | $8 | <a href="https://www.amazon.com/Arduino-A000066-ARDUINO-UNO-R3/dp/B008GRTSV6/"> Link </a> |
| USB cable | What the item is used for | $10 | <a href="https://www.amazon.com/Arduino-A000066-ARDUINO-UNO-R3/dp/B008GRTSV6/"> Link </a> |
| Jumper wires | What the item is used for | $7 | <a href="https://www.amazon.com/Arduino-A000066-ARDUINO-UNO-R3/dp/B008GRTSV6/"> Link </a> |
| Accelerometer | What the item is used for | $20 | <a href="https://www.amazon.com/Arduino-A000066-ARDUINO-UNO-R3/dp/B008GRTSV6/"> Link </a> |
| Piezo Buzzer | What the item is used for | $3 | <a href="https://www.amazon.com/Arduino-A000066-ARDUINO-UNO-R3/dp/B008GRTSV6/"> Link </a> |
| 100 ohm resistor  | What the item is used for | $0.10 | <a href="https://www.amazon.com/Arduino-A000066-ARDUINO-UNO-R3/dp/B008GRTSV6/"> Link </a> |
| 10 kohm resistor  | What the item is used for | $0.06 | <a href="https://www.amazon.com/Arduino-A000066-ARDUINO-UNO-R3/dp/B008GRTSV6/"> Link </a> |
| Breadboard | What the item is used for | $2.5` | <a href="https://www.amazon.com/Arduino-A000066-ARDUINO-UNO-R3/dp/B008GRTSV6/"> Link </a> |
| Knee sleeve | What the item is used for | $Price | <a href="https://www.amazon.com/Arduino-A000066-ARDUINO-UNO-R3/dp/B008GRTSV6/"> Link </a> |


# Other Resources/Examples
One of the best parts about Github is that you can view how other people set up their own work. Here are some past BSE portfolios that are awesome examples. You can view how they set up their portfolio, and you can view their index.md files to understand how they implemented different portfolio components.
- [Example 1](https://trashytuber.github.io/YimingJiaBlueStamp/)
- [Example 2](https://sviatil0.github.io/Sviatoslav_BSE/)
- [Example 3](https://arneshkumar.github.io/arneshbluestamp/)

To watch the BSE tutorial on how to create a portfolio, click here.
