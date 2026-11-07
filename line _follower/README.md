# Maze-Solving Line Follower

This directory contains the main Arduino sketch for the two-pass maze-solving robot. It uses five analog IR sensors for line detection, PID correction for line tracking, and a left-hand-priority strategy to explore the maze.

## How it works

1. Select **explore/record** mode and start a run with the pause button. At junctions, the robot prioritizes a left turn, records its decisions, and records dead ends as U-turns.
2. On reaching the endpoint, the robot simplifies the recorded route and signals completion by blinking the LED.
3. Select **replay** mode and start another run without restarting the Arduino. The robot uses the in-memory route to navigate the maze.

The recorded route is stored in RAM and is lost when the board is reset or powered off. Replay mode is unavailable until a route has been recorded during the current session.

## Hardware and pin assignments

| Component | Arduino Uno pin |
|---|---|
| IR sensor: far left | A0 |
| IR sensor: left | A4 |
| IR sensor: center | A1 |
| IR sensor: right | A2 |
| IR sensor: far right | A3 |
| Pause button | D2 |
| Explore/replay mode switch | D4 |
| Left/right motor enable | D5 / D6 |
| Left motor direction | D7 / D8 |
| Right motor direction | D9 / D10 |
| Completion LED | D11 |

Both switches use `INPUT_PULLUP`. A HIGH reading on the mode switch selects explore/record mode; LOW selects replay mode. The pause button is also active-low.

## Configuration

Open `line_follower.ino` in the Arduino IDE, select **Arduino Uno**, and upload the sketch. Tune `THRESHOLD` and `WHITE_IS_HIGH` for the sensor polarity and track surface. Adjust `BASE_SPEED`, `TURN_SPEED`, and the `KP`, `KI`, and `KD` gains to suit the robot and course.

The endpoint is detected when all five sensor readings indicate white. Calibrate sensor polarity and threshold before running the maze.
