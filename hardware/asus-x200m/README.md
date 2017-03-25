# Changing Backlight not working

Source: https://bugs.launchpad.net/ubuntu/+source/linux/+bug/1329510

WORKAROUND: Backlight can be set with xbacklight after creating `/usr/share/X11/xorg.conf.d/20-intel.conf` :
```
Section "Device"
    Identifier "card0"
    Driver "intel"
    Option "Backlight" "intel_backlight"
    BusID "PCI:0:2:0"
EndSection
```
but special keys are not working, and there are no events in acpi_listen when pressing these keys.

To get special keys working in the file `/etc/default/grub`, you'll see a line that looks like this:

`GRUB_CMDLINE_LINUX_DEFAULT="quiet splash"`

All you want to do is add two parameters to that line to make it look like this:

`GRUB_CMDLINE_LINUX_DEFAULT="quiet splash acpi_os_name=Linux acpi_osi="`

That's it. Save the file and run sudo update-grub in a terminal. Reboot, and your brightness keys should start working perfectly.
