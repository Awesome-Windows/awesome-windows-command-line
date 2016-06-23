# <img src="https://raw.githubusercontent.com/Awesome-Windows/awesome-windows-command-line/master/media/awesome-terminal.gif" width="400" alt="awesome windows">

[![Awesome](https://cdn.rawgit.com/sindresorhus/awesome/d7305f38d29fed78fa85652e3a63e154dd8e8829/media/badge.svg)](https://github.com/sindresorhus/awesome) [![ghit.me](https://ghit.me/badge.svg?repo=Awesome-Windows/awesome-windows-command-line)](https://ghit.me/repo/Awesome-Windows/awesome-windows-command-line)

> An awesome & curated list of commands in Windows.

## Table of Contents

- [Appearance](#appearance)
    - [Wallpaper](#wallpaper)
- [System Configuration](#system-configuration)
    - [Hibernation](#hibernation)
    - [Serial Number](#serial-number)
    - [Computer Name](#computer-name)
    - [WiFi](#wifi)
    - [Firewall](#firewall)
    - [Time Zone](#time-zone)

## Appearance

### Wallpaper

#### Set Wallpaper
```
reg add "HKEY_CURRENT_USER\Control Panel\Desktop" /v Wallpaper /t REG_SZ /d  wallpaper_path /f

RUNDLL32.EXE user32.dll,UpdatePerUserSystemParameters
 
* Works only for bmp images. If you have .jog or .jpeg images you can’t set them as wallpaper from command line.*

```

## System Configuration

### Hibernation

#### Enable/Disable Hibernation

```
powercfg /hibernate on
powercfg /hibernate off

* Should be run from adminstrator command line. *
```

### Serial Number

#### serial number for RAM, motherboard, hard disk

```

wmic memorychip get serialnumber
wmic diskdrive get serialnumber
wmic baseboard get serialnumber
wmic cdrom where drive='d:' get SerialNumber
```

### Computer Name

#### Changing Computer Name from command line.

```
WMIC computersystem where caption='currentname' rename newname
```

### WiFi

#### Disable WiFi connection

```
netsh interface set interface name="Wireless Network Connection" admin=DISABLED
```

### Firewall

#### Enable/Disable Firewall

```
* For XP/Server 2003 *

netsh firewall set opmode mode=ENABLE
netsh firewall set opmode mode=DISABLE

* For later versions *

netsh advfirewall set currentprofile state on
netsh advfirewall set  currentprofile state off

netsh advfirewall set domainprofile state on
netsh advfirewall set domainprofile state off

netsh advfirewall set privateprofile state on
netsh advfirewall set privateprofile state off

netsh advfirewall set publicprofile state on
netsh advfirewall set publicprofile state off

netsh advfirewall set  allprofiles state on
netsh advfirewall set  allprofiles state off

* These above commands should be run from adminstrator command line. *
```

### Time Zone

#### Set Time Zone

```
* Windows 7 *

tzutil /s  "Time zone Identifier"

* Here, Time zone Identifier could be Pacific Standard Time, Central America Standard Time. *

* Get the current Time Zone. *

tzutil /g

* Get the list of Time Zones. *

tzutil /l

* In Windows XP *

RunDLL32.exe shell32.dll,Control_RunDLL timedate.cpl,,/Z Central Standard Time

```
