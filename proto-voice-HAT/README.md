# Proto Voice HAT

A custom, DIY voice HAT prototype for Raspberry Pi, built with commonly available parts like Adafruit and SparkFun breakout boards etc..  
V1 has a single microphone, a 3W amp for audio output and a RGB LED to indicate different states.

![proto-hat-phase-01](images/proto-hat-phase-01.jpg)

# Resources

## HAT and Breakout Boards

- [Adafruit Perma-Proto HAT for Pi Mini Kit - With EEPROM](https://github.com/adafruit/Adafruit-Perma-Proto-HAT-PCB)
- [Adafruit I2S MEMS Microphone Breakout](https://learn.adafruit.com/adafruit-i2s-mems-microphone-breakout)
- [Adafruit MAX98357 I2S Class-D Mono Amp](https://learn.adafruit.com/adafruit-max98357-i2s-class-d-mono-amp)
- [SparkFun WS2812B RGB LED Breakout](https://github.com/sparkfun/WS2812_Breakout)

## Google AIY Voice HAT

The original AIY voice HAT by Google uses most of the components mentioned above so we can study the schematics to learn some tricks :-)

- [Voice HAT mic and board schematics](https://github.com/google/aiyprojects-raspbian/tree/aiyprojects/schematics/voice_hat)
- [Driver support for Google voiceHAT soundcard](https://github.com/raspberrypi/linux/pull/1923/files) (Raspberry Pi Linux commit)

# Credits

- [custom-voice-hat](https://github.com/shivasiddharth/custom-voice-hat) by by shivasiddharth - Foundation for this project
