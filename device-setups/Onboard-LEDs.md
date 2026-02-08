# On-Board LED Setup

## Armbian Bullseye (Feb 27, 2023) - Orange-Pi

- On-board status LEDs are controlled via `/sys/class/leds/status_led/`
- Use `cat /sys/class/leds/status_led/trigger` to see all options. The value in brackets is the active option `[...]`
- Set the new active value for example via:
  - `echo "disk-activity" | sudo tee /sys/class/leds/status_led/trigger` as sudo user
  - or simply `echo "disk-activity" > /sys/class/leds/status_led/trigger` as root
- The file will be reset at boot, to make changes permanent you can add the command to `/etc/rc.local` as root (before exit)
