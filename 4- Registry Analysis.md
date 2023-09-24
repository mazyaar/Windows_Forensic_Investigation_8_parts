# Windows Forensic Investigation (4- Registry Analysis) :ice_cube:

## Prerequisites

We reached the fourth step of Windows forensics process, needless to mention the importance of the previous phases:

> 1- ***Gathering Volatile Information:  [**link**](https://github.com/mazyaar/Windows_Forensic_Investigation_8_parts/blob/main/1-%20Gathering%20Volatile%20Information.md)***
> 
> ***2- Collecting Non-volatile Information:  [**link**](https://github.com/mazyaar/Windows_Forensic_Investigation_8_parts/blob/main/2-%20Collecting%20Non-volatile%20Information.md)***
> 
> ***3- Memory Analysis:  [**link**](https://github.com/mazyaar/Windows_Forensic_Investigation_8_parts/blob/main/3-%20Memory%20Analysis.md)***

## Definition

>**The Windows registry is an organized database with low-level settings for Microsoft Windows OS and applications that use it. Analyzing the data in the registry can assist forensic investigators in gathering information on software installation, hardware driver configuration, user activity, and connected devices. This information is useful for creating a timeline analysis of an incident during a forensic investigation.**

## ***1/ Get Informed***

_The first step is to get informed about the Windows registry. It can take forever to understand it fully as it is a complex subject, but you don’t need to be an expert in registry to get the information you’re looking for._

_Windows Registry is composed of  **5 hives** that contain everything:_

![](https://miro.medium.com/v2/resize:fit:700/1*hmQ-GDR82UdiHxRrtc9G7Q.png)

**Registry Editor**

### ***HKEY_USERS (HKU):***

_Contains information about all currently active users (SID) profiles. keys and values under each SID control the user specific mapped drives, installed printers, environmental variables, and so on._

### ***HKEY_LOCAL_MACHINE (HKLM):***

_Contains software configuration information and information about the physical state of the computer. It’s data is stored in_
```
“%SystemRoot%\Users\<UserName>”\NTUSER.DAT
```
### ***HKEY_CLASSES_ROOT (HKCR):***

_Subkey of HKLM\Software. Contains the information that ensure that the correct program opens when the user opens a file through Windows Explorer._

### ***HKEY_CURRENT_USER (HKCU):***

Contains the configuration information related to the user currently logged-on (wallpaper, display settings)

### ***HKEY_CURRENT_CONFIG (HKCC):***

_Stores information about the current hardware profile of the system. explains the differences between the current and standard hardware configuration.  **A pointer**  to_
```HKLM\SYSTEM\CurrentControlSet\Hardware Profiles\Current```

**· Non-volatile Hives are:**  ``HKEY_LOCAL_MACHINE``, ``HKEY_USERS``

 **· Volatile Hives:**  ``HKEY_CLASSES_ROOT``, ``HKEY_CURRENT_USER``, ``HKEY_CURRENT_CONFIG``

> ***Identify which hives are relevant to your investigation***

# 2/ Types of Forensic Analysis

_The Windows registry is a valuable resource for digital forensic investigations as it allows investigators to extract various types of forensic artifacts, including user accounts, recently accessed files, USB activity, last run programs, and installed applications._

_There are two methods of analyzing Windows Registry:_

### ***A- Static Analysis***

_Check the registry files inside C:\Windows\System32\config folder stored on the captured evidence file_

![C:\Windows\System32\config](https://miro.medium.com/v2/resize:fit:700/1*Wcq6Q9HieDL5aWXVOH7xew.png)

***C:\Windows\System32\config***

**1- DEFAULT:**  **_includes default user settings_**

**2- SAM (Security Account Manager):**  **_includes local user account and local group membership information like passwords._**

**3- SECURITY:**  **_stores information on the current user security policy_**

**4- SOFTWARE:** **_holds information about installed applications and their configuration on the system_**

**5- SYSTEM:** **_holds configuration settings of hardware drivers and services_**

_after gathering needed files use tools like  [**Hex Workshop**](http://www.hexworkshop.com/)  to retrieve artifacts related to cyber-crimes (SSH installed the day of the attack !!)_

![Hex Workshop](https://miro.medium.com/v2/resize:fit:700/1*ObvK5MdHD4baway-Vrdqpg.png)

### SOFTWARE Subkey Analysis

**we can also export registry to a text file**

![](https://miro.medium.com/v2/resize:fit:700/1*nqQ5B0fwGTb6ZqIJCmR3TQ.png)

![](https://miro.medium.com/v2/resize:fit:700/1*RsihlcfV1JTWdvXwr_BVsw.png)

_The registry can be considered as a log file as it has some action or event associated with a time like  **Last Write Time** which provides a timeframe reference for certain user activities on the system._

![](https://miro.medium.com/v2/resize:fit:700/1*shL7o14ZtaJjfUhN1wGiHg.png)

## B- Live Analysis

_Investigators can access the registry using  **the built-in registry editor**, as well as capture registry files from a live system using tools such as  [**FTK Imager**](https://www.exterro.com/ftk-imager)  for further analysis._

_Open FTK Imager > Add Evidence Item > Logical Drive > Next_

![](https://miro.medium.com/v2/resize:fit:700/1*O9q3_yEUNhef62sD7qEGjA.png)

_browse to C:\Windows\System32\config > choose the registry file you want to investigate._

![](https://miro.medium.com/v2/resize:fit:700/1*xfeUqHN0gBbYLhGBEjqLKA.png)

# 3/ Valuable Information Locations

### _1. System Information_

- Computer Name  
``HKLM\SYSTEM\CurrentControlSet\Control\ComputerName\ActiveComputerName``
  
- ProductName, CurrentBuildNumber, RegisteredOwner, etc.  
``HKLM\SOFTWARE\Microsoft\Windows NT\CurrentVersion``

## _2. Last Shutdown Time and Time Zone_

- Last Shutdown Time  
``HKLM\SYSTEM\ControlSet001\Control\Windows``
- Timezone Settings   
``HKLM\SYSTEM\CurrentControlSet\Control\TimeZoneInformation`` 

_Use  [DCode](https://www.digital-detective.net/dcode/)  to convert found data to human-readable format._

![](https://miro.medium.com/v2/resize:fit:700/1*HlcmAbF6xWLFUw6XQa8e8A.png)

### 3. Shares

``HKLM\SYSTEM\CurrentControlSet\Services\LanmanServer\Shares``

_By default, Windows Vista, 7, 8.1, and 10 create hidden administrative shares on a system. If a user creates an additional share, it’llappear here._

![](https://miro.medium.com/v2/resize:fit:700/1*DeeiUciNXoPc6Vf6Im_p1Q.png)

### 4. Wireless SSIDs

``HKLM\SOFTWARE\Microsoft\Windows NT\CurrentVersion\NetworkList\Profiles\{GUID}``

_This key will give you information about any accessed wireless networks: their names, first time of connection, last time of connection, etc._

![](https://miro.medium.com/v2/resize:fit:700/1*a_v8jszJ7npusA2J7qiaBg.png)

### 5. Startup Locations

``[HKCU|HKLM]\SOFTWARE\Microsoft\Windows\CurrentVersion\Run``

_Search for any unusual programs that appears in the auto startup list._

![](https://miro.medium.com/v2/resize:fit:700/1*tCxIG0TeM0RWU6bySAV_fQ.png)

_in the case of live analysis you can use: Task Manager > Startup apps,_

_you can use  [**Autoruns**](https://learn.microsoft.com/en-us/sysinternals/downloads/autoruns)  or  [**Slient Runners**](https://silentrunners.org/)  to enumerate autostart locations (use  [**VirusTotal**](https://www.virustotal.com/)  to analyze files and URLs for viruses, worms, trojans and other kinds of malicious content)._

![Autoruns utility](https://miro.medium.com/v2/resize:fit:700/1*3Hf-3OqeTXLtEukqgqDiWw.png)

### 6. User Login

``HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Run``
``HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\RunOnce``
``HKCU\SOFTWARE\Microsoft\Windows\CurrentVersion\Run``
``HKCU\SOFTWARE\Microsoft\Windows\CurrentVersion\RunOnce``

_When a user logs into a system, these keys are accessed and parsed so that the startup apps can be executed, so it gives an idea about when the user logged-in. they’re not accessed if the system is started in  **Safe Mode.**_

### 7. Microsoft Security ID

``HKLM\SOFTWARE\Microsoft\Windows NT\CurrentVersion\ProfileList``

_a unique identification number (acts as a token) that Microsoft assigns to a Windows user account for granting user access to a specific resource._

### 8. User Activity

``HKLM\SOFTWARE\Classes\exefile\shell\open\command``   
``HKCR\exefile\shell\open\command``

_Autostart registry locations are accessed when the user performs any action like opening an application, so search them for malicious code._

``HKLM\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Winlogon\Notify`` 

>_Windows sends alerts when certain events occurs (logged-on/off), based on Last Write times check entries close to the date of the suspected incident._

``HKLM\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Winlogon\Userinit``
``HKLM\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Winlogon\Shell``

>_these are also commonly abused Winlogon registry keys and value for persistence like Notify,_

_check (in the previous 3 keys) for entries that list DLLs in the DLLName value that have suspicious file version information or no file version information at all._

### 9. USB Removable Storage Devices

_After a USB device is plugged into a Windows system, the PnP (Plug and Play) manager searches for the required driver to recognize the device, and evidence of its use, such as artifacts or footprints, can be found in the registry._

``HKLM\SYSTEM\CurrentControlSet\Enum\USBSTOR``  
``HKLM\SYSTEM\CurrentControlSet\Control\DeviceClasses``

_export these two keys to text files and use both unique instance identifier  **(GUID)**  and the  **ParentIdPrefix**  to determine the last time when the USB device was connected to the system. You can also use  [**USBDeview**](https://www.nirsoft.net/utils/usb_devices_view.html)  to view the contents of the device descriptor._

### 10. Mounted Devices

_When a device is mounted on an NTFS system, it’s assigned a driver letter_

``HKLM\System\MountedDevices``

### 11. The User Assist Keys

_When a user access a file, control panel applets, and programs:_

``HKCU\Software\Microsoft\Windows\CurrentVersion\Explorer\UserAssist\{GUID}\Count``

![](https://miro.medium.com/v2/resize:fit:700/1*mR_Cm6shpTQqmrE3qc1PVg.png)

values are encoded in ROT-13 encryption algorithm (Caesar cipher), use  [**rot13**](https://rot13.com/)  to decode it.

![](https://miro.medium.com/v2/resize:fit:664/1*HCWoHW97YrnxdCiZgO1alw.png)

_registry keys that track user activities can be found in the  **NTUSER.DAT** file._

### 12. MRU Lists

``HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\RecentDocs``  
``HKCU\Software\Microsoft\Windows\CurrentVersion\Explorer\RunMRU``  
``HKCU\Software\Microsoft\Windows\CurrentVersion\Explorer\ComDlg32``

![](https://miro.medium.com/v2/resize:fit:700/1*InxTYiU2XJTZqI2V6Myz7w.png)

_The  **RunMRU**  key is added when a user execute a program from Start > Run._

_HKCU\Software\Microsoft\Internet Explorer\TypedURLs_

_contains the typed URLs into the address bar of Internet Explorer (Edge)_

### 13. Connecting to Other Systems

``HKCU\Software\Microsoft\Windows\CurrentVersion\Explorer\Map Network Drive MRU ``

_when the system connects to a remote drive or share using  **Map Network Drive Wizard**, an MRU List is added._

``HKCU\Software\Microsoft\Windows\CurrentVersion\Explorer\MountPoints2``

_contains the remote drives added using either  **Map Network Drive Wizard**  or the  **net use**  command._
