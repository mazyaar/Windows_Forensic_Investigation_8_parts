# Windows Forensics: (6–7 Examine Windows Files and Metadata) :abacus:
![](https://miro.medium.com/v2/resize:fit:700/1*Ea2VKvLkpDmllUIeFU08CQ.png)

***The Windows forensics methodology comprises of 8 phases, and we have previously covered the initial five. If you wish to explore them further, you can refer to the provided links.***

> _1- Gathering Volatile Information:  [link](https://github.com/mazyaar/Windows_Forensic_Investigation_8_parts/blob/main/1-%20Gathering%20Volatile%20Information.md
)_
> 
> _2- Collecting Non-volatile Information:  [link](https://github.com/mazyaar/Windows_Forensic_Investigation_8_parts/blob/main/2-%20Collecting%20Non-volatile%20Information.md)_
> 
> _3- Memory Analysis:  [link](https://github.com/mazyaar/Windows_Forensic_Investigation_8_parts/blob/main/3-%20Memory%20Analysis.md)_
> 
> 4- Registry Analysis:  [link](https://github.com/mazyaar/Windows_Forensic_Investigation_8_parts/blob/main/4-%20Registry%20Analysis.md)
> 
> 5- Cache, Cookies, and History Analysis:  [link](https://github.com/mazyaar/Windows_Forensic_Investigation_8_parts/blob/main/5-%20Examine%20the%20Cache,%20Cookies,%20and%20History%20Recorded%20in%20Web%20Browsers.md)

_During a Windows system investigation, investigators often need to identify any modifications that attackers may have made to application files on the system. To achieve this, investigators must analyze the following components:_

### Restore Point Directories:

_These directories contain information about the installation or removal of application files, as well as any changes made to them._

-   **RP.log file:**  _contains description of the event that caused the restore point creation_
-   **Change.log files:** _record file changes , which are located in the restore point directories_

### Prefetch Files:

_Examining the prefetch directory assists in identifying the applications that were executed on the system._

-   _When a user installs an application, runs it, and deletes it , traces of that application can be found in ``C:\Windows\Prefetch directory``_
-  _Number of launch times_ (``DWORD value at the offset 144``)
-   _Last launch time_ (``DWORD value at the offset 120``)
-   _Correlate information from_``.pf`` _file with the registry or Event Log information to determine logged-on users, running applications, etc._
-   _WinPrefetchView ([NirSoft.net](https://www.nirsoft.net/utils/win_prefetch_view.html#:~:text=WinPrefetchView%20is%20a%20small%20utility,the%20information%20stored%20in%20them.)) reads the Prefetch files present on the system and displays the information such as File Size, MAC Times, Run Counter, Process EXE, Process Path, Last Run Time, etc._
-   _Check if prefetching is enabled at:_ 
```
HKLM\SYSTEM\ControlSet001\Control\SessionManager\MemoryManagement\PrefetchParameters\EnablePrefetcher
```

>***0: disabled   
1: Application prefetching   
2: Boot prefetching   
3: application and boot prefetching***

### Image Files and EXIF Data:

_Analyzing JPEG image files and the EXIF data they contain can provide insight into the metadata associated with those images._

_This section outlines the process of examining these Windows files and the associated metadata._

-   _Metadata on JPEG image file depends on the application that created or modified it_
-   _Digital cameras embed Exchangeable Image File Format (EXIF) information in images, including GPS data, device model, serial Number, etc._
-   _[ExifReader](https://www.npmjs.com/package/exifreader#:~:text=ExifReader%20is%20a%20JavaScript%20library,(depending%20on%20file%20type).),  [EXIF Library](https://libexif.github.io/), and  [ExifTool](https://exiftool.org/)  display EXIF data found in a JPEG image._
-   _Use Exiv2 ([exiv2.org](https://exiv2.org/)) or IrfanView ([IrfanView.com](https://www.irfanview.com/)) to view, retrieve, or even modify image metadata._

### Metadata:

_Metadata associated with any file type reveals various characteristics and finer details related to the creation, access, and modification of files._

-   ***Users may unintentionally disclose confidential information when sharing or providing electronic files because such information is often not readily visible***

-  ***Examples of metadata: Organization name, Author name, Computer name, Network name, Hidden text or cells, MAC times (modified, accessed, and created)***
-   ***Copy a file: retains the same modification date, but updates creation date to the current date***
-   ***Move a file: retains the same modification and creation date***
-   ***$STANDARD_INFO (SI) can be modified by user level processes $FILE_NAME (FN) can only be modified by the system kernel***
-   ***You can use the Perl scripts pdfmeta.pl and pdfdmp.pl to extract metadata from PDF files (author name, creation date and application, if the file was created on a Mac or by converting from a Word file)***
-   ***You can use the Perl scripts wmd.pl and oledmp.pl to list the OLE streams embedded in a Word document (up to last 10 editors, past revisions)***
-   ***Use tools such as Metadata Assistant, Paraben P2 Commander, and  [Metashield Analyzer](https://metashieldclean-up.elevenpaths.com/)  to analyze metadata***

# Other Locations

### ShellBags:

-   ***Windows OS can track the view preferences of folders such as its size, position, and location that have been visited by the user via Windows Explorer***
-   ***These view preferences are stored in Windows OS as Registry keys known as “ShellBags”***
-   ***Bags key: ```HKCU\Software\Microsoft\Windows\Shell\Bags -> view preferences```***
-   ***BagMRU:_ ```HKCU\Software\Microsoft\Windows\Shell\BagMRU``` -> _tracks recently accessed directories, even after the directory is removed, which can be used to enumerate previously mounted drives, deleted files and User/Intruder actions.***
-   ***Use ShellBags Explorer ([github/ericzimmerman](https://ericzimmerman.github.io/)), ShellBagsView ([NirSoft](https://www.nirsoft.net/utils/shell_bags_view.html)), SBag ([tzworks](https://tzworks.com/download_links.php)) to browse ShellBag data***

### LNK Files:

-   ***The investigator can get valuable insights on user activities analyzing shortcut files in ```C:\Users\[TargetUser]\AppData\Roaming\Microsoft\Windows\Recent directory```***
-   Use Lnk Explorer ***([github/ericzimmerman](https://github.com/EricZimmerman/LECmd)) to decode information contained in shortcut files.***
```
LECmd -d C:\Users\ TargetUser]\AppData\Roaming\Microsoft\Windows\Recent -q - -csv .\
```
### Analyzing Jump Lists:

-   ***A taskbar feature of Windows 7 and above versions that provides the user with a graphical interface to the recently accessed applications, files and performed actions***
-   **AutomaticDestinations:**  ``C:\Users\[TargetUser]\AppData\Roaming\Microsoft\Windows\Recent\AutomaticDestinations (created automatically by the OS)``
-   **CustomDestinations:**  ``C:\Users\[TargetUser]\AppData\Roaming\Microsoft\Windows\Recent\CustomDestinations (created when a user pins a file/program to taskbar)``
-   ***JumpListExt ([onworks.net](https://www.onworks.net/software/app-jumplistext)) is the tool that parses Jump Lists and helps investigators analyze them.***
