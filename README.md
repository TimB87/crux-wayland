my current sway setup
==================
# rough setup:
## main testing device
 - old (2013) Acer notebook using i915 mesa driver
 - running sway (wlroots-based) as a wayland compositor
    - `xwayland disabled`
 - greetd with tuigreet
 - seatd
 - basu (sdbus compat library and userspace handler)
 - pipewire-pulse
 - rofi, mako, i3statusbar-rust
 - am i forgetting something..?
## desktop
 - old i5 with amdgpu (RX580)
 - sway with `xwayland enabled`
 - same software otherwise

# Preperation
Some steps when you switch from any X11 WM/DM:
## ports  
Compile some ports to offer wayland support or make life easier. a list that may or may not be complete or completely unnecessary. 
Maybe in that order:
 - wayland-protocols
 - libdrm
 - libglvnd
 - libva
    - maybe dependent ports as well?
 - mesa
 - gtk3
 - seatd
    - allows us not having to set `suid-bit` on sway
 - basu
 - greetd
 - xdg-desktop-portal
    - choosing from existing portals as you need them
 - sway

Of course including matching `-32`-counterparts that you might have installed
## variables 
Something needs to set `XDG_RUNTIME_DIR` for you, e.g. `contrib/pam_xdg`.

In short, it likes to be set to `/run/user/${UID}`, which by design is a tmpfs and will hold sockets and other runtime dirs. Read more about it here: [XDG Base Directory Specification](https://specifications.freedesktop.org/basedir-spec/basedir-spec-latest.html)

# starting sway

 - started with greetd, which will start a little script called start-sway

### `/usr/local/bin/start-sway`

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
