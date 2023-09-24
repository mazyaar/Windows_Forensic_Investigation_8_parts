
# Windows Forensic Investigation (2- Collecting Non-volatile Information) :bulb:
## _**Intro**_

_As discussed in a previous post, the investigation process in a Windows machine has 8 steps that begins with gathering volatile data and ends with analyzing text-based logs and Windows event logs._

***you can read about the first step***  [**here**](https://bit.ly/3DqDcTQ)**.**

## Definition

_The focus of the second stage is collecting non-volatile data, or the data that persists even after the system has been shut down._

_Hard drives are where non-volatile data is typically stored, however it can also be found in swap files, slack space, and unallocated storage space. Smart phones, USB storage devices, and CD-ROMs are other non-volatile data storage devices._

_Examples of non-volatile data are: photos, emails, pdf and word documents, spreadsheets and other valuable “deleted” files._

## Steps

_You can use these steps to conduct non-volatile data collection:_

### _**1.**_  _**Examining File Systems**_
```
dir /o:d 
```
_to check the time and date of the OS installation, check finished automatic update and to give priority to recently dated files._

### _**2.**_  _**Examine Extensible Storage Engine (ESE) Database**_

_ESE is used by many Microsoft software like Active Directory, Windows Mail, Windows Search, and Windows Update Client, etc._

***· ESEDatabaseView ([nirsoft.net](https://www.nirsoft.net/utils/ese_database_view.html))***

_to view and analyze ‘.edb’ files such as:_

**Windows Search Index:** 
``C:\ProgramData\Microsoft\Search\Data\Applications\Windows\windows.db``

**Windows updates information:** ``C:\windows\SoftwareDistribution\DataStore\DataStore.edb``

## _**3.**_  _**Detecting Externally Connected Devices to the System**_

· ***DriveLetterView ([nirsoft.net](https://www.nirsoft.net/utils/drive_letter_view.html))***

_to list all the drives even currently unplugged._

· ***DevCon.exe ([Microsoft](https://learn.microsoft.com/en-us/windows-hardware/drivers/devtest/devcon#:~:text=DevCon%20(Devcon.exe)%2C,%2C%20configure%2C%20and%20remove%20devices.))***

_to document devices that are attached to the system._

### _**4.**_  _**Slack Space**_

· ***DriveSpy ([Digital Intelligence](https://digitalintelligence.com/))***

_to collect all the slack space in an entire partition into a file._

### _**5.**_  _**Collecting Hidden Partition Information**_

· ***find & mount ([findandmount.com](http://findandmount.com/download/))*** 
· ***Partition Logic ([partitionlogic.org.uk](https://partitionlogic.org.uk/))***

***to collect the information from the hidden partition and to perform many useful tasks on partitions.***

### ***6.***  ***Web Browser Cache, Cookies, Temporary Files***

· ***Chrome cache view ([nirsoft.net](https://www.nirsoft.net/utils/chrome_cache_view.html))***
· ***MZ cache view ([nirsoft.net](https://www.nirsoft.net/utils/mozilla_cache_viewer.html))***
· ***Chrome cookies view ([nirsoft.net](https://www.nirsoft.net/utils/chrome_cookies_view.html))***
· ***MZ cookies view ([nirsoft.net](https://www.nirsoft.net/utils/mzcv.html))***

***[nirsoft.net](https://www.nirsoft.net/)  offers efficient tools to view cache and cookies of most of web browsers.***

## ***7.***  ***Analyzing Windows Thumbnail Cache***

· ***Thumbcache Viewer ([github](http://thumbcacheviewer.github.io/))***
· ***Thumbs Viewer ([github](https://thumbsviewer.github.io/))***

_to open thumbcache_***.db files inside_ ``C:\Users\UserProfile]\AppData\Local\Microsoft\Windows\Explorer directory for example.``

