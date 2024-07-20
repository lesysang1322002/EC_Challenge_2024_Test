Leanbot API Reference
---

[Arduino basic reference](https://www.arduino.cc/reference/en/)

[Leanbot](#Leanbot)
- [Leanbot.begin](#Leanbot.begin)
- [LbDelay (blocking)](#LbDelay-%28blocking%29)
- [LbMission.begin (blocking)](#LbMission.begin-%28blocking%29)
- [LbMission.beginDigitalTwin (blocking)](#LbMission.beginDigitalTwin-%28blocking%29)
- [LbMission.end (blocking)](#LbMission.end-%28blocking%29)
- [LbMission.elapsedMillis](#LbMission.elapsedMillis)


[Motion (actuator)](#Motion-%28actuator%29)
- [LbMotion.runLR](#LbMotion.runLR)
- [LbMotion.runLRrpm](#LbMotion.runLRrpm)
- [LbMotion.stopAndWait (blocking)](#LbMotion.stopAndWait-%28blocking%29)
- [LbMotion.isStop](#LbMotion.isStop)
- [LbMotion.isMoving](#LbMotion.isMoving)
- [LbMotion.waitDistance (blocking)](#LbMotion.waitDistance-%28blocking%29)
- [LbMotion.waitDistanceMm (blocking)](#LbMotion.waitDistanceMm-%28blocking%29)
- [LbMotion.waitRotation (blocking)](#LbMotion.waitRotation-%28blocking%29)
- [LbMotion.waitRotationDeg (blocking)](#LbMotion.waitRotationDeg-%28blocking%29)
- [LbMotion.getDistance](#LbMotion.getDistance)
- [LbMotion.getDistanceMm](#LbMotion.getDistanceMm)
- [LbMotion.getRotation](#LbMotion.getRotation)
- [LbMotion.getRotationDeg](#LbMotion.getRotationDeg)


[Gripper (actuator)](#Gripper-%28actuator%29)
- [LbGripper.open (blocking)](#LbGripper.open-%28blocking%29)
- [LbGripper.close (blocking)](#LbGripper.close-%28blocking%29)
- [LbGripper.moveTo (blocking)](#LbGripper.moveTo-%28blocking%29)
- [LbGripper.moveToLR (blocking)](#LbGripper.moveToLR-%28blocking%29)
- [LbGripper.readL](#LbGripper.readL)
- [LbGripper.readR](#LbGripper.readR)


[Buzzer (actuator)](#Buzzer-%28actuator%29)
- [Leanbot.tone](#Leanbot.tone)
- [Leanbot.noTone](#Leanbot.noTone)


[RGB Leds (actuator)](#RGB-Leds-%28actuator%29)
- [LbRGB.show](#LbRGB.show)
- [LbRGB.clear](#LbRGB.clear)
- [LbRGB[ ]](#LbRGB[-])
- [LbRGB.fillColor](#LbRGB.fillColor)


[Touch Sensors](#Touch-Sensors)
- [LbTouch.read](#LbTouch.read)
- [LbTouch.readBits](#LbTouch.readBits)
- [LbTouch.onPress](#LbTouch.onPress)


[Ultrasonic Sensor](#Ultrasonic-Sensor)
- [Leanbot.pingCm](#Leanbot.pingCm)
- [Leanbot.pingMm](#Leanbot.pingMm)


[IR Sensors](#IR Sensors)
- [LbIRLine.read](#LbIRLine.read)
- [LbIRLine.value](#LbIRLine.value)
- [LbIRLine.print](#LbIRLine.print)
- [LbIRLine.displayOnRGB](#LbIRLine.displayOnRGB)
- [LbIRLine.isBlackDetected](#LbIRLine.isBlackDetected)
- [LbIRLine.doManualCalibration (blocking)](#LbIRLine.doManualCalibration-%28blocking%29)
- [LbIRArray.read](#LbIRArray.read)


[DC Motor (actuator)](#DC-Motor-%28actuator%29)
- [Leanbot.DCMotor.setPower](#Leanbot.DCMotor.setPower)


[Leanbot IoT](README_LeanbotIoT.md)

&nbsp;
---

# Leanbot

## Leanbot.begin

### Description
This function initializes Leanbot

### Syntax
```
Leanbot.begin()
```

### Parameters
None

### Returns
None

### Example
```
#include <Leanbot.h>

void setup() {
  Leanbot.begin();                // initialize Leanbot
}
```

### Notes and Warnings
This function must be called at the beginning in the `setup` function.

[🔼 Back to top](#leanbot-api-reference)
&nbsp;
---

[[ Leanbot ]](#Leanbot)
## LbDelay (blocking)

### Description
This function makes the program wait (blocking the program flow) until a specified delay time has elapsed, then process the next line of code.
In the meantime, Leanbot keeps running at current velocities.

### Syntax
```
LbDelay(timeMs)
```

### Parameters
- `timeMs`: the number of milliseconds to wait (1000 milliseconds equals one second)
  - Unit: ms
  - Range: [0, 65535]
  - Allowed data types: `unsigned int`

### Returns
None

### Example
This example makes Leanbot moves forward at speed of 400 for 3 seconds, then stop
```
LbMotion.runLR(400, 400);    // let Leanbot move forward
LbDelay(3000);               // wait for 3 seconds (Leanbot keeps moving forward)
LbMotion.runLR(0, 0);        // stop Leanbot
```

### Notes and Warnings
The maximum delay time is `65,535` milliseconds (≈ 65.5 seconds)

[🔼 Back to top](#leanbot-api-reference)
&nbsp;
---

[[ Leanbot ]](#Leanbot)
## LbMission.begin (blocking)

### Description
Leanbot waits (blocking the program flow) for the signal to start the mission by simultaneously touching both `TB1A` and `TB1B` buttons on the front of Leanbot.

When receiving the start signal:
- Leanbot will emit the countdown sound `3` – `2` – `1`
- then starts the mission, do tasks

### Syntax
```
LbMission.begin()
```

### Parameters
None

### Returns
None

### Example
```
LbMission.begin();
```

[🔼 Back to top](#leanbot-api-reference)
&nbsp;
---

[[ Leanbot ]](#Leanbot)
## LbMission.beginDigitalTwin (blocking)

### Description
This function sends the mission name to the server, then Leanbot waits (blocking the program flow) for the signal to start the mission by one of the following:
- Click the `Start` button on the Digital Twin web interface
- Or simultaneously touch both `TB1A` and `TB1B` buttons on the front of Leanbot

When receiving the start signal:
- Leanbot will emit the countdown sound `3` – `2` – `1`
- then starts the mission, do tasks

### Syntax
```
LbMission.beginDigitalTwin(F( missionId ))
```

### Parameters
- `missionId`: the name of mission
  - Allowed data types: `string`

### Returns
None

### Example
```
LbMission.beginDigitalTwin(F( "ms11.1" ));
```
See more:
- [MissionDigitalTwin_ms1.1.ino](examples/LbMission/MissionDigitalTwin_ms1.1.ino)

[🔼 Back to top](#leanbot-api-reference)
&nbsp;
---

[[ Leanbot ]](#Leanbot)
## LbMission.end (blocking)

### Description
This function
- Stop Leanbot, end of mission
- Stop the program flow completely

### Syntax
```
LbMission.end()
```

### Parameters
None

### Returns
None

### Example
```
LbMission.end();
```
See more:
- [MissionDigitalTwin_ms1.1.ino](examples/LbMission/MissionDigitalTwin_ms1.1.ino)

### Notes and Warnings
Leanbot does not run any code after this function

[🔼 Back to top](#leanbot-api-reference)
&nbsp;
---

[[ Leanbot ]](#Leanbot)
## LbMission.elapsedMillis

### Description
This function returns the elapsed time since Leanbot started the mission.

### Syntax
```
elapsedTimeMs = LbMission.elapsedMillis()
```

### Parameters
None

### Returns
The elapsed time since Leanbot started the mission
- Unit: ms
- Data type: `long`

### Example
```
long elapsedTimeMs = LbMission.elapsedMillis();
```

[🔼 Back to top](#leanbot-api-reference)
&nbsp;
---


# Motion (actuator)
![Screenshot](image/Motion.png)

## LbMotion.runLR

### Description
This function sets the speed and direction of rotation for the left and right wheels.
The greater the speed, the faster the wheel rotates.

### Syntax
```
LbMotion.runLR(vL, vR)
```

### Parameters
- `vL`: left wheel velocity
- `vR`: right wheel velocity
  - Unit: steps per second
  - Range: [-2000, +2000]
  - Positive value: rotate forward
  - Negative value: rotate backward
  - Allowed data types: `int`

### Returns
None

### Example
This example makes Leanbot moves forward at speed of 400
```
LbMotion.runLR(400, 400);
```
See more:
- [runLR.ino](examples/LbMotion/runLR.ino)

[🔼 Back to top](#leanbot-api-reference)
&nbsp;
---

[[ Leanbot ]](#Leanbot) / [[ Motion (actuator) ]](#Motion-%28actuator%29)
## LbMotion.runLRrpm

### Description
This function sets the speed (in revolutions per minute) and direction of rotation for the left and right wheels.
The greater the number of revolutions per minute, the faster the wheel rotates.

### Syntax
```
LbMotion.runLRrpm(rpmL, rpmR)
```

### Parameters
- `rpmL`: left wheel velocity
- `rpmR`: right wheel velocity
  - Unit: RPM - revolutions per minute
  - Range: [-60, +60]
  - Positive value: rotate forward
  - Negative value: rotate backward
  - Allowed data types: `int`

### Returns
None

### Example
This example makes Leanbot moves forward at 30 revolutions per minute
```
LbMotion.runLRrpm(30, 30);
```
See more:
- [runLRrpm.ino](examples/LbMotion/runLRrpm.ino)

[🔼 Back to top](#leanbot-api-reference)
&nbsp;
---

[[ Leanbot ]](#Leanbot) / [[ Motion (actuator) ]](#Motion-%28actuator%29)
## LbMotion.stopAndWait (blocking)

### Description
This function stops Leanbot and waits (blocking the program flow) until Leanbot has decelerated to a complete stop.

### Syntax
```
LbMotion.stopAndWait()
```

### Parameters
None

### Returns
None

### Example

```
LbMotion.stopAndWait();
```

### Notes and Warnings
The higher the speed the Leanbot is running, the longer it takes to stop. The distance traveled before stopping will also be longer.

[🔼 Back to top](#leanbot-api-reference)
&nbsp;
---

[[ Leanbot ]](#Leanbot) / [[ Motion (actuator) ]](#Motion-%28actuator%29)
## LbMotion.isStop

### Description
This function checks if Leanbot has stopped or not.

### Syntax
```
isStop = LbMotion.isStop()
```

### Parameters
None

### Returns
- `true`: Leanbot has stopped
- `false`: Leanbot is moving
- Data type: `bool`

### Example
```
bool isStop = LbMotion.isStop();
```

[🔼 Back to top](#leanbot-api-reference)
&nbsp;
---

[[ Leanbot ]](#Leanbot) / [[ Motion (actuator) ]](#Motion-%28actuator%29)
## LbMotion.isMoving

### Description
This function checks if Leanbot is moving or not.

### Syntax
```
isStop = LbMotion.isMoving()
```

### Parameters
None

### Returns
- `true`: Leanbot is moving
- `false`: Leanbot has stopped
- Data type: `bool`

### Example
```
bool isMoving = LbMotion.isMoving();
```

[🔼 Back to top](#leanbot-api-reference)
&nbsp;
---

[[ Leanbot ]](#Leanbot) / [[ Motion (actuator) ]](#Motion-%28actuator%29)
## LbMotion.waitDistance (blocking)

### Description
The program waits (blocking the program flow) in this function until Leanbot travels the desired distance in steps.
Then process the next line of code.

### Syntax
```
LbMotion.waitDistance(distanceStep)
```

### Parameters
- `distanceStep`: the number of steps to wait for Leanbot to travel
  - Unit: steps
  - Allowed data types: `long`

### Returns
None

### Example

```
LbMotion.runLR(400, 400);       // let Leanbot move forward
LbMotion.waitDistance(1500);    // wait for Leanbot to advance 1500 steps
```
See more:
- [waitDistance.ino](examples/LbMotion/waitDistance.ino)

[🔼 Back to top](#leanbot-api-reference)
&nbsp;
---

[[ Leanbot ]](#Leanbot) / [[ Motion (actuator) ]](#Motion-%28actuator%29)
## LbMotion.waitDistanceMm (blocking)

### Description
The program waits (blocking the program flow) until Leanbot has moved by (approximately) distance in millimeters.
Then process the next line of code.

### Syntax
```
LbMotion.waitDistanceMm(distanceMm)
```

### Parameters
- `distanceMm`: the distance in millimeters to travel
  - Unit: mm
  - Allowed data types: `int`

### Returns
None

### Example

```
LbMotion.runLR(400, 400);       // let Leanbot move forward
LbMotion.delayDistanceMm(150);  // wait for Leanbot to advance 150mm = 15cm
```
See more:
- [waitDistanceMm.ino](examples/LbMotion/waitDistanceMm.ino)

[🔼 Back to top](#leanbot-api-reference)
&nbsp;
---

[[ Leanbot ]](#Leanbot) / [[ Motion (actuator) ]](#Motion-%28actuator%29)
## LbMotion.waitRotation (blocking)

### Description
The program waits (blocking the program flow) until Leanbot has rotated by (approximately) the desired steps.
Then process the next line of code.

### Syntax
```
LbMotion.waitRotation(rotationStep)
```

### Parameters
- `rotationStep`: the number of differential steps to wait for Leanbot to rotate
  - Unit: steps
  - Allowed data types: `long`

### Returns
None

### Example

```
LbMotion.runLR(+400, -400);      // let Leanbot rotate
LbMotion.waitRotation(1500);     // wait for rotating 1500 steps
```
See more:
- [waitRotation.ino](examples/LbMotion/waitRotation.ino)

### Notes and Warnings
Experiment and rotation adjustment are required to find the step value corresponding to the desired rotation angle
- The step value will be different for each Leanbot, speed and moving surface
- For example: with speed 500 and rotation value is 1750, Leanbot will rotate an angle of approximately 90°

[🔼 Back to top](#leanbot-api-reference)
&nbsp;
---

[[ Leanbot ]](#Leanbot) / [[ Motion (actuator) ]](#Motion-%28actuator%29)
## LbMotion.waitRotationDeg (blocking)

### Description
The program waits (blocking the program flow) until Leanbot has rotated by (approximately) the desired degrees.
Then process the next line of code.

### Syntax
```
LbMotion.waitRotationDeg(rotationDeg)
```

### Parameters
- `rotationDeg`: the angle to wait for Leanbot to rotate
  - Unit: degree (angle)
  - Allowed data types: `int`

### Returns
None

### Example
```
LbMotion.runLR(+500, -500);        // let Leanbot rotate right
LbMotion.waitRotationDeg(180);     // wait for Leanbot to rotate approximately 180°
```

[🔼 Back to top](#leanbot-api-reference)
&nbsp;
---

[[ Leanbot ]](#Leanbot) / [[ Motion (actuator) ]](#Motion-%28actuator%29)
## LbMotion.getDistance

### Description
This function returns the distance in number of steps which Leanbot has traveled from origin

### Syntax
```
long distance = LbMotion.getDistance()
```

### Parameters
None

### Returns
The traveled distance in number of steps
- Unit: steps
- Data type: `long`

### Example
```
long distance = LbMotion.getDistance();
```

[🔼 Back to top](#leanbot-api-reference)
&nbsp;
---

[[ Leanbot ]](#Leanbot) / [[ Motion (actuator) ]](#Motion-%28actuator%29)
## LbMotion.getDistanceMm

### Description
This function returns the distance in millimeters which Leanbot has traveled from origin

### Syntax
```
long distance = LbMotion.getDistanceMm()
```

### Parameters
None

### Returns
The traveled distance in millimeters
- Unit: mm
- Data type: `long`

### Example
```
long distanceMm = LbMotion.getDistanceMm();
```

[🔼 Back to top](#leanbot-api-reference)
&nbsp;
---

[[ Leanbot ]](#Leanbot) / [[ Motion (actuator) ]](#Motion-%28actuator%29)
## LbMotion.getRotation

### Description
This function returns the angle in number of steps which Leanbot has rotated from origin

### Syntax
```
long rotation = LbMotion.getRotation()
```

### Parameters
None

### Returns
The rorated angle in number of steps
- Unit: steps
- Data type: `long`

### Example
```
long rotation = LbMotion.getRotation();
```

[🔼 Back to top](#leanbot-api-reference)
&nbsp;
---

[[ Leanbot ]](#Leanbot) / [[ Motion (actuator) ]](#Motion-%28actuator%29)
## LbMotion.getRotationDeg

### Description
This function returns the angle in degrees which Leanbot has rotated from origin

### Syntax
```
long rotationDegree = LbMotion.getRotationDeg()
```

### Parameters
None

### Returns
The rorated angle in degrees
- Unit: degree (angle)
- Data type: `long`

### Example
```
long rotationDegree = LbMotion.getRotationDeg();
```

[🔼 Back to top](#leanbot-api-reference)
&nbsp;
---

# Gripper (actuator)
![Screenshot](image/LbGripper.png)

## LbGripper.open (blocking)

### Description
This function moves gripper arms to open position (both arms at 0 degree position - perpendicular to the surface)

### Syntax
```
LbGripper.open()
```

### Parameters
None

### Returns
None

### Example
```
LbGripper.open();
```
See more:
- [GripperOpenClose.ino](examples/LbGripper/GripperOpenClose.ino)

[🔼 Back to top](#leanbot-api-reference)
&nbsp;
---

[[ Leanbot ]](#Leanbot) / [[ Gripper (actuator) ]](#Gripper-%28actuator%29)
## LbGripper.close (blocking)

### Description
This function moves gripper arms to close position (both arms at 90 degree position - parallel to the surface)


### Syntax
```
LbGripper.close()
```

### Parameters
None

### Returns
None

### Example
```
LbGripper.close();
```
See more:
- [GripperOpenClose.ino](examples/LbGripper/GripperOpenClose.ino)

[🔼 Back to top](#leanbot-api-reference)
&nbsp;
---

[[ Leanbot ]](#Leanbot) / [[ Gripper (actuator) ]](#Gripper-%28actuator%29)
## LbGripper.moveTo (blocking)

### Description
This function moves both gripper arms to the same desired angle.

### Syntax
```
LbGripper.moveTo(toAngle)
```

### Parameters
- `toAngle`: the degree to move to
  - Unit: degree (angle)
  - Range: [-30, +120]
  - Allowed data types: `int`

### Returns
None

### Example
The example moves both the gripper arms to the position 45°
```
LbGripper.moveTo(45);
```
See more:
- [GripperMoveTo.ino](examples/LbGripper/GripperMoveTo.ino)

[🔼 Back to top](#leanbot-api-reference)
&nbsp;
---

[[ Leanbot ]](#Leanbot) / [[ Gripper (actuator) ]](#Gripper-%28actuator%29)
## LbGripper.moveToLR (blocking)

### Description
This function moves both gripper arms to their desired angles for a desired amount of time (blocking the program flow).

### Syntax
```
LbGripper.moveToLR(toAngleL, toAngleR, timeMs)
```

### Parameters
- `toAngleL`: the degree for left gripper arm to move to
- `toAngleR`: the degree for right gripper arm to move to
  - Unit: degree (angle)
  - Range: [-30, +120]
  - Allowed data types: `int`

- `timeMs`: the time in milliseconds to move both grippers to the target angles
  - Allowed data types: `int`

### Returns
None

### Example
The example moves the left gripper to position 30° and the right gripper to position 60° for 1.5 seconds
```
LbGripper.moveToLR(30, 60, 1500);
```
See more:
- [GripperMoveToLR.ino](examples/LbGripper/GripperMoveToLR.ino)

[🔼 Back to top](#leanbot-api-reference)
&nbsp;
---

[[ Leanbot ]](#Leanbot) / [[ Gripper (actuator) ]](#Gripper-%28actuator%29)
## LbGripper.readL

### Description
This function returns the current angle (in degrees) of the left gripper arm.

### Syntax
```
LbGripper.readL()
```

### Parameters
None

### Returns
The current angle (in degrees) of the left gripper arm
- Unit: degree (angle)
- Range: [-30, +120]
- Data type: `int`

### Example
```
int angleL = LbGripper.readL();
```

[🔼 Back to top](#leanbot-api-reference)
&nbsp;
---

[[ Leanbot ]](#Leanbot) / [[ Gripper (actuator) ]](#Gripper-%28actuator%29)
## LbGripper.readR

### Description
This function returns the current angle (in degrees) of the right gripper arm.

### Syntax
```
LbGripper.readR()
```

### Parameters
None

### Returns
The current angle (in degrees) of the right gripper arm
- Unit: degree (angle)
- Range: [-30, +120]
- Data type: `int`

### Example
```
int angleR = LbGripper.readR();
```

[🔼 Back to top](#leanbot-api-reference)
&nbsp;
---

# Buzzer (actuator)

## Leanbot.tone

### Description
This function plays sounds with the specified frequency in a duration of time.
- While playing the sound, Leanbot continues to process the next line of code
- The sound will automatically stop after the duration, or call the [Leanbot.noTone](#Leanbot.noTone) function

### Syntax
```
Leanbot.tone(frequency, duration)
```

### Parameters
- frequency: the frequency of the tone in Herzt (Hz)
  - Unit: Herzt (Hz)
  - Allowed data types: `unsigned int`

- duration: (optional) the duration of the tone in milliseconds
  - Unit: ms
  - Allowed data types: `unsigned int`

### Returns
None

### Example
Play sound with frequency 1000 Hz for 1.5 s
```
Leanbot.tone(1000, 1500);
```
See more:
- [tone.ino](examples/Buzzer/tone.ino)
- [toneDuration.ino](examples/Buzzer/toneDuration.ino)

### Notes and Warnings
This function is non-blocking, which means that even if you provide the duration parameter
the sketch execution will continue immediately even if the tone hasn't finished playing.

[🔼 Back to top](#leanbot-api-reference)
&nbsp;
---

[[ Leanbot ]](#Leanbot) / [[ Buzzer (actuator) ]](#Buzzer-%28actuator%29)
## Leanbot.noTone

### Description
This function stops the sound played by [Leanbot.tone](#Leanbot.tone)

### Syntax
```
Leanbot.noTone()
```

### Parameters
None

### Returns
None

### Example
```
Leanbot.noTone();
```
See more:
- [noTone.ino](examples/Buzzer/noTone.ino)

[🔼 Back to top](#leanbot-api-reference)
&nbsp;
---

# RGB Leds (actuator)
![Screenshot](image/LbRGB.png)
- Leanbot has 7 RGB Leds: `ledA`, `ledB`, `ledC`, `ledD`, `ledE`, `ledF` and `ledO`

## RGB color code
There are 3 different syntax to represent a RGB color:
1. Color name: `CRGB::ColorName`
  - Example: `CRGB::Red`, `CRGB::Green`, `CRGB::Blue`
  - See more: [https://github.com/FastLED/FastLED/wiki/Pixel-reference#predefined-colors-list](https://github.com/FastLED/FastLED/wiki/Pixel-reference#predefined-colors-list)

2. Decimal code: `CRGB(red, green, blue)`
  - Each parameter (red, green, and blue) defines the intensity of the color with a value between 0 and 255
  - Example:
    - `CRGB(255, 0, 0)` is red, because red is set to highest value (255), and the other two (green and blue) are set to 0
    - `CRGB(0, 255, 0)` is green, because green is set to highest value (255), and the other two (red and blue) are set to 0
    - To display black, set all parameters to 0: `CRGB(0, 0, 0)`
    - To display white, set all parameters to 255: `CRGB(255, 255, 255)`
  - See more: [https://www.w3schools.com/colors/colors_picker.asp](https://www.w3schools.com/colors/colors_picker.asp)

3. Hex code: `0xRRGGBB`
  - Concatenate the 3 hex values of the red, green and blue together
  - Example: `0xFF0000` (red), `0x00FF00` (green), `0x0000FF` (blue)

## LbRGB.show

### Description
This function shows all Leds to diplay.

### Syntax
```
LbRGB.show()
```

### Parameters
None

### Returns
None

### Example
```
LbRGB.show();
```

### Notes and Warnings
This function must be called after updating the color of the Leds.

[🔼 Back to top](#leanbot-api-reference)
&nbsp;
---

[[ Leanbot ]](#Leanbot) / [[ RGB Leds (actuator) ]](#RGB-Leds-%28actuator%29)
## LbRGB.clear

### Description
This function clears all Leds to black.

### Syntax
```
LbRGB.clear()
```

### Parameters
None

### Returns
None

### Example
```
LbRGB.clear();
```

[🔼 Back to top](#leanbot-api-reference)
&nbsp;
---

[[ Leanbot ]](#Leanbot) / [[ RGB Leds (actuator) ]](#RGB-Leds-%28actuator%29)
## LbRGB[ ]

### Description
This function sets a led to the given RGB color.

### Syntax
```
LbRGB[ledX] = color
```

### Parameters
- `ledX`: the led to be set
- `color`: the [RGB color code](#RGB-color-code)

### Returns
None

### Example
```
LbRGB[ledA] = CRGB::Red;              // set `ledA` to red
LbRGB[ledO] = CRGB(0, 255, 0);        // set `ledO` to green
LbRGB[ledD] = 0x0000FF;               // set `ledD` to blue
LbRGB.show();                         // show all Leds to diplay
```
See more:
- [setColor.ino](examples/LbRGB/setColor.ino)

### Notes and Warnings
This function only updates the color value of a led
- You have to call [LbRGB.show](#LbRGB.show) to make the leds actually show the new colors

[🔼 Back to top](#leanbot-api-reference)
&nbsp;
---

[[ Leanbot ]](#Leanbot) / [[ RGB Leds (actuator) ]](#RGB-Leds-%28actuator%29)
## LbRGB.fillColor

### Description
This function fills a shape (set of Leds) with a given RGB color.

### Syntax
```
LbRGB.fillColor(color, shape)
```

### Parameters
- `color`: the [RGB color code](#RGB-color-code)

- `shape`: a set of Leds to be set
  - Allowed data types: `byte`

### Returns
None

### Example
The example sets the 4 Leds A, B, C and D (a smiley shape) to green
```
byte LbSmiley = BITMAP(ledA, ledB, ledC, ledD);   // create smiley shape
LbRGB.fillColor(CRGB::Green, LbSmiley);           // fill green color
LbRGB.show();                                     // show all Leds to diplay
```
See more:
- [fillColor.ino](examples/LbRGB/fillColor.ino)

[🔼 Back to top](#leanbot-api-reference)
&nbsp;
---

# Touch Sensors
![Screenshot](image/LbTouch.png)
- Leanbot has 4 touch sensors: `TB1A`, `TB1B`, `TB2A` and `TB2B`

## LbTouch.read

### Description
This function reads the state of the specified touch sensors.

### Syntax
```
value = LbTouch.read(tbX)
```

### Parameters
`tbX`: the touch sensor to read. Valid choices are:
- TB1A
- TB1B
- TB2A
- TB2B

### Returns
The state the touch sensor
- Value `0`: the sensor is being released
- Value `1`: the sensor is being touched
- Data type: `byte`

### Example
The example reads the state of the sensors `TB1A` and `TB2A`
```
byte value1A = LbTouch.read(TB1A);
byte value2A = LbTouch.read(TB2A);
```
See more:
- [ledControl.ino](examples/LbTouch/ledControl.ino)
- [wheelControl.ino](examples/LbTouch/wheelControl.ino)

### Notes and Warnings
Multiple sensors can be combined and read at once time.
```
LbTouch.read(TB1A | TB1B)
```

[🔼 Back to top](#leanbot-api-reference)
&nbsp;
---

[[ Leanbot ]](#Leanbot) / [[ Touch Sensors ]](#Touch-Sensors)
## LbTouch.readBits

### Description
This function reads the state of all 4 touch sensors.

### Syntax
```
touchBits = LbTouch.readBits()
```

### Parameters
- None

### Returns
The binary state of 4 touch sensors
- Value `0`: the sensor is being released
- Value `1`: the sensor is being touched
- Data type: `byte`

### Example
```
byte touchBits = LbTouch.readBits();
```
See more:
- [readBits.ino](examples/LbTouch/readBits.ino)

[🔼 Back to top](#leanbot-api-reference)
&nbsp;
---

[[ Leanbot ]](#Leanbot) / [[ Touch Sensors ]](#Touch-Sensors)
## LbTouch.onPress

### Description
This function reads the touching event of the specified touch sensors.

### Syntax
```
isOnPress = LbTouch.onPress(tbX)
```

### Parameters
- `tbX`: the touch sensor to read

### Returns
The touching event the touch sensor
- Value `true`: the sensor has NOT just been touched, either released or being held
- Value `false`: the sensor has just been touched
- Data type: `bool`

### Example
The example reads the touching state of the sensor `TB1A`
```
bool value1A = LbTouch.onPress(TB1A);
```
See more:
- [onPress.ino](examples/LbTouch/onPress.ino)

### Notes and Warnings
Multiple sensors can be combined and read at once time.
```
LbTouch.onPress(TB1A | TB1B)
```

[🔼 Back to top](#leanbot-api-reference)
&nbsp;
---

# Ultrasonic Sensor

### Notes and Warnings
The ultrasonic sensor can be triggered as fast as every 50 ms, or 20 times each second
- You should wait 50 ms before the next ping
- This is to ensure the ultrasonic __beep__ has faded away and will not cause a false echo on the next ranging

## Leanbot.pingCm

### Description
This function sends a ping and returns the front distance measured in centimeters.

### Syntax
```
distanceCm = Leanbot.pingCm()
```

### Parameters
None

### Returns
The front distance measured in centimeters
- Unit: cm
- Data type: `unsigned int`

### Example
```
unsigned int distanceCm = Leanbot.pingCm();
```
See more:
- [pingCm.ino](examples/Ping/pingCm.ino)

### Notes and Warnings
The maximum sensor distance is 300 cm, outside this distance, the function will return 1,000 cm.

[🔼 Back to top](#leanbot-api-reference)
&nbsp;
---

[[ Leanbot ]](#Leanbot) / [[ Ultrasonic Sensor ]](#Ultrasonic-Sensor)
## Leanbot.pingMm

### Description
This function sends a ping and returns the front distance measured in millimeters.

### Syntax
```
distanceMm = Leanbot.pingMm()
```

### Parameters
None

### Returns
The front distance measured in centimeters
- Unit: mm
- Data type: `unsigned int`

### Example
```
unsigned int distanceMm = Leanbot.pingMm();
```

### Notes and Warnings
The maximum sensor distance is `3,000 mm`, outside this distance, the function will return `10,000 mm`

[🔼 Back to top](#leanbot-api-reference)
&nbsp;
---

# IR Sensors

![Screenshot](image/LbIRArray.png)
- Leanbot has 8 IR sensors (order 0 - 7), for different purposes:

| Function             | Sensors                   |
| -------------------- |:-------------------------:|
| Line detection       | ir3R - ir1R - ir0L - ir2L |
| Table edge detection | ir5R - ir4L               |
| Obstacles detection  | ir7R - ir6L               |

## LbIRLine.read

### Description
This function reads the value of 4 bar sensors. Used to check the position of the black line relative to Leanbot.

### Syntax
```
lineState = LbIRLine.read()
```

### Parameters
None

### Returns
The binary state of 4 bar sensors
- Value `0`: the sensor is on the white surface
- Value `1`: the sensor is on the black line
- Data type: `byte`

### Example
```
byte lineState = LbIRLine.read();
```
See more:
- [readLineState.ino](examples/LbIRLine/readLineState.ino)
- [followLine.ino](examples/LbIRLine/followLine.ino)

[🔼 Back to top](#leanbot-api-reference)
&nbsp;
---

[[ Leanbot ]](#Leanbot) / [[ IR Sensors ]](#IR-Sensors)
## LbIRLine.value

### Description
This function returns the value of 4 bar sensors which are read before.

### Syntax
```
LbIRLine.value()
```

### Parameters
None

### Returns
The 4 line sensors value
- Data type: `byte`

### Example
```
byte lineValue = LbIRLine.value();
```

[🔼 Back to top](#leanbot-api-reference)
&nbsp;
---

[[ Leanbot ]](#Leanbot) / [[ IR Sensors ]](#IR-Sensors)
## LbIRLine.print

### Description
This function sends the value of the 4 bar sensors (which are read before) to the computer.

### Syntax
```
LbIRLine.print()
```

### Parameters
None

### Returns
None

### Example
```
LbIRLine.print();
```

[🔼 Back to top](#leanbot-api-reference)
&nbsp;
---

[[ Leanbot ]](#Leanbot) / [[ IR Sensors ]](#IR-Sensors)
## LbIRLine.displayOnRGB

### Description
This function displays the 4 bar sensors result on RGB Leds with color.
- If any sensor is on the black line, the corresponding RGB Led will light up

### Syntax
```
LbIRLine.displayOnRGB(color)
```

### Parameters
- `color`: the [RGB color code](#RGB-color-code)

### Returns
None

### Example
```
LbIRLine.read();                     // update line state
LbIRLine.displayOnRGB(CRGB::Blue);   // display result on Leds
```

[🔼 Back to top](#leanbot-api-reference)
&nbsp;
---

[[ Leanbot ]](#Leanbot) / [[ IR Sensors ]](#IR-Sensors)
## LbIRLine.isBlackDetected

### Description
This function checks whether one of the 4 bar sensors is on the black line.

### Syntax
```
LbIRLine.isBlackDetected()
```

### Parameters
None

### Returns
- `true` : the bars sensor is on the black line
- `false`: the bars sensor is NOT on the black line
- Data type: `bool`

### Example
The example lets Leanbot moving forward until the end of the black line
```
LbMotion.runLR(400, 400);                // move forward
while ( LbIRLine.isBlackDetected() );    // keep moving as long as Leanbot can see the black line
LbMotion.stopAndWait();                  // stop
```

[🔼 Back to top](#leanbot-api-reference)
&nbsp;
---

[[ Leanbot ]](#Leanbot) / [[ IR Sensors ]](#IR-Sensors)
## LbIRLine.doManualCalibration (blocking)

### Description
This function does 3-step light level calibration with touch button.

### Syntax
```
LbIRLine.doManualCalibration(tbX)
```

### Parameters
- `tbX`: the touch sensor used to perform black/white sampling
  - Leanbot has 4 touch sensors: `TB1A`, `TB1B`, `TB2A` and `TB2A`

### Returns
None

### Example
```
LbIRLine.doManualCalibration(TB1A);
```
See more:
- [lineCalibration.ino](examples/LbIRLine/lineCalibration.ino)
- [calibrationThenFollowLine.ino](examples/LbIRLine/calibrationThenFollowLine.ino)

### Notes and Warnings
It is recommended to perform this step before starting the mission or when there are changes in ambient light or moving surface.

[🔼 Back to top](#leanbot-api-reference)
&nbsp;
---

## LbIRArray.read

### Description
This function reads the value of the specified sensor.
The darker the surface, the higher the sensor value.

### Syntax
```
LbIRArray.read(irX)
```

### Parameters
- `irX`: the sensor to read

### Returns
The sensor value: 0 - 768
- Data type: `int`

### Example
The example reads the value of sensor `ir0L` and sends the result to the computer
```
int value = LbIRArray.read(ir0L);    // read the sensor value
Serial.println(value);               // transfer the results to the computer
```

[🔼 Back to top](#leanbot-api-reference)
&nbsp;
---

# DC Motor (actuator)

## Leanbot.DCMotor.setPower

### Description
This function makes the motor rotates at a desired speed in the forward or backward direction.
The greater the power, the faster the motor rotates.

### Syntax
```
Leanbot.DCMotor.setPower(power)
```

### Parameters
- `power`: the power level
  - Range: [-255, +255]
  - Positive integer: turn forward
  - Negative integer: turn backward
  - 0: turn off
  - Allowed data types: `int`

### Returns
None

### Example
The code makes the motor rotates forward at power level of 250
```
Leanbot.DCMotor.setPower(250);
```
See more:
- [setPower.ino](examples/DCMotor/setPower.ino)

### Notes and Warnings
Values out of range will be constrained between -255 and +255

[🔼 Back to top](#leanbot-api-reference)
&nbsp;
---
