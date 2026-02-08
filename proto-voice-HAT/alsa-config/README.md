# ALSA Config for Proto Voice HAT

This ALSA config applies several tweaks:
- Use dmix and dsnoop to allow multiple devices access at the same time
- Register volume control for `alsamixer`
- Use LADSPA high-pass filter on mic signal to remove initial fall-off and center DC signal
- Boost the microphone signal to acceptable level
- Set correct default

## Install

- Make sure that you have ALSA filters installed: `sudo apt install swh-plugins`
- Copy the config to your system AND user folder (just to make sure):
  - `sudo cp asound.conf /etc/asound.conf`
  - `cp asound.conf ~/.asoundrc`

## Known issues

- The Proto Voice HAT has a cold start issue and requires about 1.5s to stabilize, which happens at a DC offset. The high-pass filter fixes this behavior, mostly, but leaves about a 100ms pop at the start of a recording.
