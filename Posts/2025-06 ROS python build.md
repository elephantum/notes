ament_python relies on `--editable` switch in setup.py to do editable install, very old stuff, deprecated a long time ago
```
Starting >>> webrtc_bridge
--- stderr: webrtc_bridge
usage: setup.py [global_opts] cmd1 [cmd1_opts] [cmd2 [cmd2_opts] ...]
   or: setup.py --help [cmd1 cmd2 ...]
   or: setup.py --help-commands
   or: setup.py cmd --help

error: option --editable not recognized
---
Failed   <<< webrtc_bridge [4.06s, exited with code 1]

Summary: 0 packages finished [4.48s]
  1 package failed: webrtc_bridge
  1 package had stderr output: webrtc_bridge
```

TODO: update ament_python to be able to build pyproject.toml based projects

https://github.com/ament/ament_cmake/issues/382
https://discourse.ros.org/t/call-for-testing-standards-based-python-packaging-with-colcon/32008