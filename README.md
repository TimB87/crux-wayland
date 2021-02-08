current sway setup
==================

- start with greetd
- custom `start-sway` command which holds some special variables 
  ```bash
  #!/bin/sh
  export XDG_CURRENT_DESKTOP=sway
  export XDG_SESSION_TYPE=wayland
  export ELM_ACCEL=gl
  export ELM_DISPLAY=wl
  export GTK_THEME=Adapta-Nokto-Eta-Maia
  export _JAVA_AWT_WM_NONREPARANTING=1

  #exec strace sway -d 2> /tmp/sway1.log
  #exec sway -d -V 2> /tmp/sway1.log
  #exec dbus-run-session -- sway -d -V 2> /tmp/sway.log
  exec dbus-run-session -- sway
  ```
