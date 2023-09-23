# Notes about running ROS 2 on steamdeck

## Motivation

Steamdeck is a great platform to be used as a controller for mobile robots. It would be great to have a setup in which steamdeck screen can be used to display camera from a robot and joysticks to control said robot.

## Ideal configuration

Steamdeck:
* runs joystick capture node and publishes `/joy` topic
* runs Foxglove for visualization

Robot:
* subscribes to `/joy` and does stuff

## Current findings

* Stable ubuntu 22.04 does not recognize steamdeck joystick as `js0` device, because 22.04 has kernel 6.2 and steamdeck joystick is supported starting from 6.3
* Steamdeck OS runs 6.3 kernel and correctly initializes `js0`
* This guy (https://github.com/ARK-Electronics/ark_rover_demo/tree/main) runs ubuntu 22.04 in container on top of steamdeck OS
* Foxglove is easy to run on top of ubuntu (Foxglove snap package)

* This guy (https://www.youtube.com/watch?v=KbF4r7yCCds) suggests using RoboStack

* In order for steamdeck joystick to work in `joy` node, you need to switch input to "joystick" in Steam in desktop mode
* How to install distrobox on steamdeck: https://www.gamingonlinux.com/2022/09/distrobox-can-open-up-the-steam-deck-to-a-whole-new-world/