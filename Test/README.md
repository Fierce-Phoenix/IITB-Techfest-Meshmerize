# Line-Follower Test Sketch

This directory contains an alternative Arduino sketch for testing line following, junction handling, and endpoint detection. Unlike the main maze-solving sketch, it does not record or replay a route.

## How it works

- Uses five digital IR sensor inputs and weighted proportional steering to keep the line centered.
- Probes junctions by creeping forward to determine whether a straight path is available.
- Prefers straight paths; when a turn is required, it selects the left branch by default (`PREFER_LEFT`).
- After detecting a branch, treats a sustained all-white reading within a time window as the endpoint and lights the red LED.
- If the line is lost, searches in the last known direction and stops if it cannot recover the line before the timeout.

The robot starts when either switch changes from OFF to ON. `SWITCH_ACTIVE_LOW` controls switch polarity; by default the switches are active-low and use the Arduino's internal pull-ups.

## Hardware and pin assignments

| Component | Arduino Uno pin |
|---|---|
| IR sensor: far left | A0 |
| IR sensor: left | A1 |
| IR sensor: center | A2 |
| IR sensor: right | A3 |
| IR sensor: far right | A4 |
| Start switches | D2 and D4 |
| Right motor direction | D7 / D8 |
| Left motor direction | D10 / D9 |
| Right/left motor enable | D5 / D6 |
| Endpoint LED | D11 |

## Configuration

Open `Test.ino` in the Arduino IDE, select **Arduino Uno**, and upload the sketch. The sensors are configured as digital inputs, so verify their output polarity and wiring. Adjust `BASE_SPEED`, `KP`, `TURN_SPEED`, `CREEP_SPEED`, `PREFER_LEFT`, and the timing constants for your hardware and maze.
