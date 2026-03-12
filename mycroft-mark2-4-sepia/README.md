# Mycroft Mark II for SEPIA

If you happen to have one of the rare Mycroft Mark II (Dev Kits) and you are wondering if you could use it as SEPIA client,
then you've come to the right place.  
This repository will explain how you can install a bare bone Raspberry Pi OS on your Mark II with all the required drivers to use a SEPIA Client (or run any other custom project).

## Installation

NOTE: So far this only worked on Raspberry Pi OS **Bullseye**, so you might need to get a rather old OS version.  
  
This repository has a "fixed" version of the 'mark-ii-raspberrypi' folder found in the original [Mark-II repository](https://github.com/MycroftAI/mark-ii-product/tree/main/mark-ii-raspberrypi).  
Download and extract it it via:
- `wget https://github.com/SEPIA-Framework/sepia-open-hardware/raw/refs/heads/main/mycroft-mark2-4-sepia/mark-ii-raspberrypi.tar.gz`
- `tar -xzf mark-ii-raspberrypi.tar.gz`

Then run `./install.sh` from `mycroft-mark2-4-sepia`.

### Boot config

The installer should set this automatically, but just to make sure plz check your boot confix.txt for these lines:
```
dtparam=audio=off
...
dtoverlay=vc4-kms-v3d,noaudio
```

## Changes to the original installation process

This is a summary of the changes that where made to the original installer.  
NOTE: The paths refer to the files AFTER installation.

### Fixed user in xmos service

`sudo nano /etc/systemd/system/mycroft-xmos.service`

### Fixed run script

`sudo nano /opt/mycroft/xmos-microphone/run.sh`

- Enable the line `sh "${this_dir}/vocalfusion/vocalfusion-rpi-setup-5.2.0/resources/load_i2s_driver.sh" || true`
- Comment out the arecord check (it crashes the script and is probably not needed anymore)
- Add `sleep 1` before the first call of `vfctrl_i2c`

### Restored missing vfctrl_i2c

When the XMOS Vocalfusion installation failed the pre-build file worked (check paths):
- `sudo ln -s /home/pi/mark-ii-raspberrypi/pre-built/usr/bin/vfctrl_i2c /usr/local/bin/vfctrl_i2c`
- `sudo chmod +x /usr/local/bin/vfctrl_i2c`

### NO extra overlay in /boot/config.txt

DON'T use this: `dtoverlay=xvf3510`  
We don't use any overlay! We use `i2s_master_loader` which is loaded via the `load_i2s_driver.sh` script (see run.sh above).  
Check it via:
- `lsmod | grep i2s_master_loader`


# Alternative driver

If the installation simply doesn't work, you can try the alternative 'VocalFusionDriver' driver from [OpenVoiceOS](https://github.com/OpenVoiceOS/VocalFusionDriver.git):
```
sudo apt install git build-essential bc bison flex libssl-dev raspberrypi-kernel-headers
git clone https://github.com/OpenVoiceOS/VocalFusionDriver.git
cd VocalFusionDriver/driver
make all
sudo mkdir -p /lib/modules/$(uname -r)/extra/
sudo cp vocalfusion-soundcard.ko /lib/modules/$(uname -r)/extra/
```

# SEPIA Client Installation

Check the official installation guide for the [SEPIA DIY Client](https://github.com/SEPIA-Framework/sepia-installation-and-setup/tree/master/sepia-client-installation/rpi).  
  
**TODO:** add CLEXI support for LED control and button listeners

## Tweaks

Disable Pulseaudio:
- `systemctl --user stop pulseaudio.service`
- `systemctl --user mask pulseaudio.socket`

# Resources

- Mark II Raspberry Pi OS drivers: https://github.com/MycroftAI/mark-ii-product/tree/main/mark-ii-raspberrypi
- Dev Kit with SJ201 Daughterboard: https://github.com/MycroftAI/hardware-mycroft-mark-II/tree/master/mark-II-Rpi-devkit
- Mark II Image / Sandbox: https://github.com/MycroftAI/mark-ii-sandbox
- XMOS Vocalfusion drivers: https://github.com/xmos/vocalfusion-rpi-setup/
- OpenVoiceOS Vocalfusion drivers: https://github.com/OpenVoiceOS/VocalFusionDriver
  - Modernize: https://github.com/OpenVoiceOS/VocalFusionDriver/issues/4
