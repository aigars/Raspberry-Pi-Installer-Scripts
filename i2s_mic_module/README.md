**Driver for the Adafruit I2S MEMS Microphone**

[Product learn page on Adafruit](https://learn.adafruit.com/adafruit-i2s-mems-microphone-breakout/overview).

This repository has small changes to the original snd-i2smic-rpi driver from [Raspberry Pi install scripts](https://github.com/adafruit/Raspberry-Pi-Installer-Scripts) that allows Raspberry Pi to receive I2S BCK and LRCK from I2S source. That is necessarry to connect Ian Canada Reciever Pi card to Raspberry Pi 4B or any other I2S source that runs with its own BCK and LRCK.

[Ian Canada Receiver Pi manual](https://github.com/iancanada/DocumentDownload/blob/master/ReceiverPi/ReceiverPi/ReceiverPiUsersManual.pdf)

This is example connection:
![Raspberry Pi 4B with Ian Canada Receiver Pi](https://github.com/aigars/Raspberry-Pi-Installer-Scripts/blob/main/i2s_mic_module/connection.jpg?raw=true)

Installing as a stand-alone module
====================================

```bash
# Get needed packages
apt-get -y install git raspberrypi-kernel-headers

# Clone the repo
git clone https://github.com/aigars/Raspberry-Pi-Installer-Scripts.git

# Build and install the module
cd Raspberry-Pi-Installer-Scripts/i2s_mic_module
make clean
make
make install

# Setup auto load at boot
echo "snd-i2smic-rpi" > /etc/modules-load.d/snd-i2smic-rpi.conf
echo "options snd-i2smic-rpi rpi_platform_generation=2" > /etc/modprobe.d/snd-i2smic-rpi.conf

# Enable I2S overlay
sed -i -e 's/#dtparam=i2s/dtparam=i2s/g' /boot/config.txt

# Reboot after installing and verify with
arecord -l
```
