# User sessions
Before executing FDBuild add a file `/opt/env.sh` with:

```
# reset vars
LD_LIBRARY_PATH=
PKG_CONFIG_PATH=
ACLOCAL_PATH=

#
# drm
#
LD_LIBRARY_PATH=/opt/drm/lib:$LD_LIBRARY_PATH
PKG_CONFIG_PATH=/opt/drm/lib/pkgconfig:$PKG_CONFIG_PATH

#
# mesa
#
LD_LIBRARY_PATH=/opt/mesa/lib:$LD_LIBRARY_PATH
PKG_CONFIG_PATH=/opt/mesa/lib/pkgconfig:$PKG_CONFIG_PATH

export LIBGL_DRIVERS_PATH=/opt/mesa/lib/dri
export EGL_DRIVERS_PATH=/opt/mesa/lib

#
# wayland
#
PATH=/opt/wayland/bin:$PATH
LD_LIBRARY_PATH=/opt/wayland/lib:/opt/wayland/lib/x86_64-linux-gnu:$LD_LIBRARY_PATH
PKG_CONFIG_PATH=/opt/wayland/lib/pkgconfig:/opt/wayland/lib/x86_64-linux-gnu/pkgconfig:$PKG_CONFIG_PATH
ACLOCAL_PATH=/opt/wayland/share/aclocal:$ACLOCAL_PATH

#
# xorg
#
PATH=/opt/xorg/bin:$PATH
LD_LIBRARY_PATH=/opt/xorg/lib:$LD_LIBRARY_PATH
PKG_CONFIG_PATH=/opt/xorg/lib/pkgconfig:/opt/xorg/share/pkgconfig:$PKG_CONFIG_PATH
ACLOCAL_PATH=/opt/xorg/share/aclocal:$ACLOCAL_PATH

export PATH
export LD_LIBRARY_PATH
export PKG_CONFIG_PATH
export ACLOCAL_PATH
```

Source it in `$HOME/.zshrc` and link it from `$HOME/.config/plasma-workspace/env/gfx-env.sh`.

# SDDM

Add in `/etc/sddm.conf`:

```
[X11]
ServerPath=/opt/xorg/bin/X
```

And via `sudo systemctl edit [--runtime] sddm.service` add:

```
[Service]
Environment=LD_LIBRARY_PATH=/opt/mesa/lib:$LD_LIBRARY_PATH
Environment=LIBGL_DRIVERS_PATH=/opt/mesa/lib/dri
Environment=EGL_DRIVERS_PATH=/opt/mesa/lib
```
