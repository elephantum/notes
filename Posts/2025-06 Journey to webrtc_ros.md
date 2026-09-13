
Mention webrtc_ros in C, spent two days compiling, did make it

New approach: python implementation based on aiortc

* use pixi+robostack because I feel potential in this combo, usb_cam is present only in humble
- standalone - works on x86
- but it's humble which is extremely old
- robostack jazzy - PR to enable usb_cam + patches https://github.com/RoboStack/ros-jazzy/pull/73

* have working version

* consumes a lot of cpu: 25% of a core
	* VPX codec + imgmsg_to_cv2 eats most of it
	* try to force h264
	* actual time was spent converting from yuyv422 to rgb and then building av.Frame from it, if we check for format and pass format directly to av.Frame.from_ndarray, CPU consumption goes to 5-7%
	* forcing h264 was a mistake, if we switch it off, consumption falls to 2-3%
	![[Pasted image 20250616235122.png]]

* working prototype works, me happy

Now I see two use cases that I can pursuit:
1. Local - ROS system and browser share a network
	1. webrtc node is a typical ROS node
	2. Signaling is done via ROS services
	3. Integration between web browser and ros is done via rosbridge and roslibjs
	4. All control signals are transported via standard ROS methods via rosbrdige
2. Remote - ROS system and browser do not share a network
	1. There's a separate signaling service in the internet
	2. All communication is done via webrtc datachannel
	3. Browser application is a webrtc client, not a ros client