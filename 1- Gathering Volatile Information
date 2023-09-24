

# Windows Forensic Investigation (1- Gathering Volatile Information) :mag_right:

>_When conducting an investigation on a Windows machine there are 8 phase to go through, today we’ll discuss the first ‘Collecting Volatile Information’, and the rest will be explained in future topics_

>_Volatile information refers to data that is lost when a system is turned off; it is typically stored in system registry, cache, and RAM._

***During live data acquisition, volatile information can be acquired. The evidence gathered from volatile data can assist forensic investigators in malware analysis, inspect log and cache files, dedicate passwords, and so on. All of these can be used as evidence during a forensic investigation.***

> _Ps: install  [**pstools**](https://learn.microsoft.com/en-us/sysinternals/downloads/pstools) before starting this process, otherwise, you can install the whole  [**sysinternals**](https://learn.microsoft.com/en-us/sysinternals/downloads/sysinternals-suite) package in case it’s not installed already_

#### _**1.**_  _**System Time**_
```
time /t & date /t
```
#### _**2.**_  _**Logged-on User(s)**_
_before doing any evidence collection, we need to be sure that the system time/date is accurate because the perpetrators can change it; a simple thing can result a chaos_
```
psloggedon  
net sessions  
logonsessions [-p]
```
_It displays the active logon sessions and, if the -p option is used (for loggonsessions), the processes that are running in each session._

#### _**3.**_  _**Network Information**_
```
nbtstat [-c] 
```
_To resolve NetBios (NetBT) cache_
### _**4.**_ _**Opened files**_
```
net file
```  
· NetworkOpenedFiles ([nirsoft.net](https://www.nirsoft.net/utils/network_opened_files.html))

### _**5.**_ Network  _**connections**_
```
netstat [-ano]
```
### _**6.**_ Network status
```
Ipconfig [/all]
```  
PromiscDetect ([Vidstrom](https://vidstromlabs.com/freetools/promiscdetect/))  
Promqry ([Microsoft](https://www.microsoft.com/en-us/download/details.aspx?id=16883))

### _**7.**_ _**Process information**_

>_Task Manager (GUI)_
>_Process Explorer (sysinternals)_  
>_tasklist [/v] [/svc]_  
>_pslist [-x]_
>_listdlls_ 
>_handle_

### _**8.**_ _**Process-to-port mapping**_
```
Netstat -ano
```
### _**9.**_ _**Process memory**_

> Process Explorer (sysinternals)  
> ProcDump (sysinternals)  
> Process Dumper ([github](https://github.com/glmcdona/Process-Dump))

### _**10.**_ _**Print Spool Files**_

- Examine .SPL and .SHD files inside C:\Windows\System32\spool\PRINTERS   
  using a hex editor ([free Hex Editor Neo](https://freehexeditorneo.com/)) 

### _**11.**_ _**Shared Resources**_
```
net share
```
The ‘$’ sign in the results means that the resource is accessed locally

### _**12.**_ _**Clipboard contents**_

Check the clipboard memory (paste its content to a text file)

### _**13.**_ _**Service/driver information**_
```
wmic service list brief
```
### _**14.**_ _**Command history**_
```
doskey /history
```
***The command history get wiped when the command prompt is closed, unlike Linux OSs.***

>_Investigators must be conscious that the utilities they are using to collect other volatile information can alter the contents of the memory. Investigators can define the user(s) logged in, the timeline of a security event, the software and libraries involved, the files accessed and shared during a suspicious incident, and other details such as network information, open files, process-to-port mapping, mapped drives, command history, process information, clipboard contents, and so on based on the volatile information gathered._
