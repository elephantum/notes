# Notes about running ROS 2 on steamdeck

## Motivation

Steamdeck is a great platform to be used as a controller for mobile robots. It would be great to have a setup in which steamdeck screen can be used to display camera from a robot and joysticks to control said robot.

## Ideal configuration

Steamdeck:
* [[Steamdeck setup]]
* runs joystick capture node and publishes `/joy` topic
* runs Foxglove for visualization

Robot:
* [[Robot setup]]
* subscribes to `/joy` and does stuff

