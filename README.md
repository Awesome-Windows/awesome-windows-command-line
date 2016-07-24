[![Awesome](https://cdn.rawgit.com/sindresorhus/awesome/d7305f38d29fed78fa85652e3a63e154dd8e8829/media/badge.svg)](https://github.com/sindresorhus/awesome)
# <img src="https://raw.githubusercontent.com/Awesome-Windows/awesome-windows-command-line/master/media/awesome-terminal.gif" alt="awesome windows">

[![Awesome](https://cdn.rawgit.com/sindresorhus/awesome/d7305f38d29fed78fa85652e3a63e154dd8e8829/media/badge.svg)](https://github.com/sindresorhus/awesome)

> An awesome & curated list of commands in Windows.

## Table of Contents

- [Appearance](#appearance)
- [Automation](#automation)
    - [Wallpaper](#wallpaper)
- [System Configuration](#system-configuration)
    - [Hibernation](#hibernation)
    - [Serial Number](#serial-number)
    - [Computer Name](#computer-name)
    - [WiFi](#wifi)
    - [Firewall](#firewall)
    - [Time Zone](#time-zone)
    - [Join a Computer to Domain](#join-a-computer-to-domain)
- [user-settings](#user-settings)
    - [Auto Login](#enabledisable-auto-login)
    - [Default Printer](#set-default-printer-in-windows7)

## Appearance

### Wallpaper

#### Set Wallpaper
```
reg add "HKEY_CURRENT_USER\Control Panel\Desktop" /v Wallpaper /t REG_SZ /d  wallpaper_path /f

RUNDLL32.EXE user32.dll,UpdatePerUserSystemParameters
 
* Works only for bmp images. If you have .jog or .jpeg images you can’t set them as wallpaper from command line.*

```
## Automation

### Automatic Shutdown

```
sleep 9000; shutdown -s

OR

at 03:30:00PM shutdown -s

OR

schtasks /create /sc once /tn "auto shutdown my computer" /tr "shutdown -s" /st 15:30

* Schedule daily shutdown *

At 11:00:00PM /every:M,T,W,TH,F,SA,SU shutdown -s

* Schedule automatic resart *

at 11:00:00PM shutdown -r

* For Sleep *

sleep number_of_seconds_to_wait; shutdown -r


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

### Join a Computer to Domain

```
netdom.exe join %computername% /domain:DomainName /UserD:DomainName\UserName /PasswordD:Password

* To remove a computer from a Domain *

netdom.exe remove %computername% /domain:Domainname /UserD:DomainName\UserName /PasswordD:Password

```
Download netdom.exe from [here](http://www.microsoft.com/downloads/details.aspx?FamilyId=49AE8576-9BB9-4126-9761-BA8011FABF38&displaylang=en)

## User Settings

### Enable/Disable Auto Login

Download Autologin from [here](http://technet.microsoft.com/en-us/sysinternals/bb963905)

```
Autologon  userName domainName password
```

### Set default printer in Windows 7

```
wmic printer get name,default

* Get Default printer *

wmic printer where default='TRUE' get name

* Set Default Printer *
wmic printer where name='printername' call setdefaultprinter

```

