# Precision 5510 Hackintosh

## Specification

```
Xeon E3-1505M v5
HD Graphics P530
Quadro M1000M
FullHD
SM961 512GB
32GB DDR4
84Whr
```

## Downloads

- The installer via the App Store or [here]()
- [Clover](https://sourceforge.net/projects/cloverefiboot/)
- Clone or [download this repo](https://github.com/khuedoan98/precision-5510-hackintosh/archive/master.zip)
- Driver for wifi USB, I use [TL-WN725N V3](https://www.tp-link.com/us/support/download/tl-wn725n/#Driver) (optional)

## BIOS setup

1.5.1 or higher is recommended

Settings:

- SATA mode: AHCI
- Secure boot: disable

## Create Install USB

Remember to erase the whole disk, not only the volume

> Disk Utility > View > Show all devices > Select USB device > Erase

- Name: USB
- Format: Mac OS Extended (Journaled)

You may need to do this twice if you encounter an error in the first time

Open the Terminal

`sudo /Applications/Install\ macOS\ High\ Sierra.app/Contents/Resources/createinstallmedia --volume /Volumes/USB --applicationpath /Applications/Install\ macOS\ High\ Sierra.app --nointeraction`

Install Clover

- Location: Install macOS High Sierra
- Customize:
    - Clover for UEFI booting only

Overwrite CLOVER folder with the one in the repo

## Install macOS

Format disk to Mac OS Extended, install, then boot with Clover in USB

Install Clover on new macOS installation, then overwrite CLOVER folder

## Post Installation

### HDMI

`sudo vim /System/Library/Extensions/AppleGraphicsControl.kext/Contents/PlugIns/AppleGraphicsDevicePolicy.kext/Contents/Info.plist`

Add these lines under `ConfigMap->dict`

```
<key>Mac-A5C67F76ED83108C</key>
<string>none</string>
```

Then rebuild the cache

`sudo kextcache -i /`

Reboot

TODO: Install audio driver and wifi driver
