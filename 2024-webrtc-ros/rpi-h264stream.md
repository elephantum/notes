Managed to get working on RPi4 with hardware acceleration and latency around 100-150ms which is very good

Sender:

```
gst-launch-1.0 \
    libcamerasrc ! video/x-raw,width=640,height=480,interlace-mode=progressive" ! \
    v4l2h264enc ! "video/x-h264,level=(string)3" ! \
    rtph264pay config-interval=3 ! \
    udpsink host=192.168.0.106 port=10001
```

Receiver:

```
gst-launch-1.0 \
    udpsrc port=10001 caps="application/x-rtp" ! \
    rtph264depay ! decodebin ! videoconvert ! \
    xvimagesink
```

Failed to get VLC to receive this RTP stream, but VLC works if we use mp4 instead of rtph264 :shrug:
