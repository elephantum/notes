aiortc - пришлось форкнуть и поправить, потому что в свежей сборке rpi + ubuntu 22.04 поменялся аппаратный кодек

оказывается WebRTC - это всего лишь идея о том, что клиент и сервер, обмениваются офферами, а потом сервер инициирует RTP стрим в сторону клиента

TODO разобрать как работает rtpsession в gstreamer

[https://github.com/pgaston/teleopros2/blob/main/teleopros2/teleopros2.py](https://github.com/pgaston/teleopros2/blob/main/teleopros2/teleopros2.py)

[https://github.com/jdgalviss/jetbot-ros2/blob/main/local_server/webrtc_control/webcam.py#L12](https://github.com/jdgalviss/jetbot-ros2/blob/main/local_server/webrtc_control/webcam.py#L12)  
  
[https://gist.github.com/kueblert/fc1517fc9254e9a3cb0add7795c337f4](https://gist.github.com/kueblert/fc1517fc9254e9a3cb0add7795c337f4)

[Gamepad Tester - Check Controllers and Joysticks Online (hardwaretester.com)](https://hardwaretester.com/gamepad)

Текущая идея: сделать 