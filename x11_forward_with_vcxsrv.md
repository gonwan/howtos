### X11 Forward with VcXsrv

- Install gnome desktop on CentOS 7:
```
sudo yum groupinstall "GNOME Desktop"
```

- Install mesa drivers:
```
sudo yum install mesa-dri-drivers
```

- Edit `/etc/ssh/sshd_config`, make sure it contains:
```
X11Forwarding yes
X11UseLocalhost no
```

- [Download](https://sourceforge.net/projects/vcxsrv/) and install `XcXsrv`, run `XLaunch` --> `Multiple Windows` --> `Start no client` --> check `Clipboard`, check `Disable access control`, uncheck `Native opengl` --> Finish. The default `DISPLAY` is `${YOUR_IP}:0.0`.

- Install ibus and pinyin input method:
```
sudo yum install ibus-gtk3 ibus-libpinyin
export DISPLAY=${YOUR_IP}:0.0
ibus-setup
```
  Run `ibus-setup` to add pinyin input method. The setup UI should appear on your local X server on Windows.

- Run chromium, it should now on the local X server and ibus also works:
```
export GTK_IM_MODULE=xim
export QT_IM_MODULE=xim
export XMODIFIERS=@im=ibus
export DISPLAY=${YOUR_IP}:0.0
ibus-daemon -drx
chromium-browser --proxy-server=socks5://127.0.0.1:xxxxx &
```
