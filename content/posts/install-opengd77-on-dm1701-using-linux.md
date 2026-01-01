---
Title: Install OpenGD77 on the Baofeng DM-1701 using Linux
date: 2025-01-25
tags:
- amateur radio
- DMR
- Linux
---
## Introduction

OpenGD77 is an open source firmware for DMR transceivers designed with
amateur radio in mind. This post describes how to flash the OpenGD77
firmware on a Baofeng DM-1701 DMR radio using Linux.

## Download the firmware

The OpenGD77 firmware requires support for AMBE voice encoding and decoding
using the original manufacturer's firmware ("donor firmware") which must,
therefore, be downloaded from the following link:

- [Baofeng DM-1701 original firmware](https://www.passion-radio.com/index.php?controller=attachment&id_attachment=760)

From the downloaded ZIP file, extract the donor firmware
"MD9600-CSV(2571V5)-V26.45.bin".

Download the OpenGD77 firmware from the following link:

- [OpenGD77 firmware](https://www.opengd77.com/downloads/MDUV380_DM1701/Firmware/2dc33f6bcb4936c047a4f65ef3daf80f95ffbc0e/OpenDM1701.zip)

and uncompress it.

## Load the firmware

Create a Python virtual environment with the prerequisites for the OpenGD77
firmware loader:

```bash
linux:~> mkdir opengd77_fw_loader
linux:~> cd opengd77_fw_loader
linux:~/opengd77_fw_loader> python -m venv .
linux:~/opengd77_fw_loader> source bin/activate.csh
(opengd77_fw_loader) linux:~/opengd77_fw_loader> pip install pyusb
```

Download the OpenGD77 firmware loader script for Linux:

```bash
wget https://www.opengd77.com/downloads/Linux_tools/opengd77_stm32_firmware_loader.py
```

Copy the two firmware files (original and OpenGD77) to the current directory.

Connect the radio to the computer with the USB cable and put it into
programming mode by switching on while pressing the Orange and SK1
buttons (respectively above and below the PTT button).

Flash the OpenGD77 firmware with the following command:

```bash
(opengd77_fw_loader) linux:~/opengd77_fw_loader> python opengd77_stm32_firmware_loader.py -s "MD9600-CSV(2571V5)-V26.45.bin -m DM-1701" -f OpenDM1701.bin
```

## Running OpenGD77CPS on Linux/Wine

Download the latest version of OpenGD77CPS from the following link:

- [https://www.opengd77.com/downloads/PC_CPS/Latest/](https://www.opengd77.com/downloads/PC_CPS/Latest/)

then set the following environment variables to create a dedicated WINE
environment in the $HOME/.wine-opengd77cps directory:

```bash
linux:~> export LC_ALL=C
linux:~> export WINEARCH=win32
linux:~> export WINEPREFIX=$HOME/.wine-opengd77cps
```

Connect the radio to the PC then run the following command to install
OpenGD77CPS:

```bash
linux:~> wine downloads/radio/OpenGD77CPSInstaller_E2022.10.16.01.exe
```

Find the correct COM port assigned to the radio (assuming there are
no other cdc-acm devices connected to the PC):

```bash
linux:~> PORT=`ls -la $WINEPREFIX/dosdevices | grep ACM | awk '{print toupper($9)}'`
```

Configure the correct COM port in Windows registry:

```bash
linux:~> wine reg add "HKLM\System\CurrentControlSet\Enum\SERIAL\\${PORT}\\${PORT}" /v ClassGUID /t REG_SZ /d {4D36E978-E325-11CE-BFC1-08002BE10318}
linux:~> wine reg add "HKLM\System\CurrentControlSet\Enum\SERIAL\\${PORT}\\${PORT}" /v FriendlyName /t REG_SZ /d "OpenGD77 (${PORT})"
```

Start OpenGD77CPS:

```bash
linux:~> wine C:/Program\ Files/OpenGD77CPS/OpenGD77CPS.exe
```

## Links

- [Installing OpenGD77 with Linux](https://www.opengd77.com/viewtopic.php?t=4172)
- [OpenGD77 user guide](https://github.com/LibreDMR/OpenGD77_UserGuide/tree/master)
- [Change transmit power](https://www.opengd77.com/viewtopic.php?t=3885)
- [Calibration information](https://www.opengd77.com/viewtopic.php?t=1250)
- [Running OpenGD77CPS on Linux with Wine](https://www.nest.org.ru/2022/10/opengd77cps_on_linux/)
- [OpenGD77 Group](https://www.facebook.com/groups/OpenGD77/)
