
# Windows Forensic Investigation (3- Memory Analysis) :floppy_disk:

# Prerequisites

> _We talked already about two very important steps in the Windows forensics procedure:  [volatile](https://github.com/mazyaar/Windows_Forensic_Investigation_8_parts/blob/main/1-%20Gathering%20Volatile%20Information.md) and  [non-volatile](https://github.com/mazyaar/Windows_Forensic_Investigation_8_parts/blob/main/2-%20Collecting%20Non-volatile%20Information.md)  data acquisition, so you need to check them out before heading to next steps._

## Definition

_Once you’re completed the previous two phases, we can continue the forensics process by doing an analysis of memory._

_The analysis of memory in Windows systems is a crucial aspect of forensic investigation, which involves obtaining a dump of the physical memory, also known as RAM. By examining these memory dumps, investigators are able to uncover hidden rootkits, identify concealed objects, and detect any anomalous processes, among other things._

### ***1.***  ***Windows Crash Dump***

_A Windows crash dump file holds the information stored in a computer’s memory at the moment of a crash. This file plays a crucial role in diagnosing and pinpointing the errors in a program that caused the system to crash. It encompasses information such as stop messages, a roster of drivers that were loaded, and details about the processor that stopped._

_There are 4 types of memory dumps:_

1.  _**Automatic memory dump**_
2.  _**Complete memory dump**_
3.  _**Kernel memory dump**_
4.  _**Small memory dump**_

_To enable memory dump setting, follow these steps:_

1.  _In  **Control Panel**, select  **System and Security** >  **System**._
2.  _Select  **Advanced system settings**, and then select the  **Advanced** tab._
3.  _In the  **Startup and Recovery**  area, select  **Settings**._

![](https://miro.medium.com/v2/resize:fit:544/1*TJbbuMHlZ5aaEQXvgic3CQ.png)

***memory dump***

_You can find the automatic memory dump file at: _ 

***C:\Windows\MEMORY.DMP***

· ***notMyfault.exe [/crash] (sysinternals)***

_to manually generate a memory dump file_

**·** ***DumpChk file ([Microsoft](https://learn.microsoft.com/en-us/windows-hardware/drivers/debugger/dumpchk))***

to  analyze the memory dump

### ***2. Collecting Process Memory***

_If the crush dump doesn’t reveal any valuable information, start collecting the contents of process memory available to a RAM dump file_

**·** ***Task Manager (Microsoft)***
**·** ***Process Dumper ([github](https://github.com/glmcdona/Process-Dump))***

_to dump the entire process space alongside metadata and the process environment to the console; it redirects the output to a file or a socket_

**·** ***Userdump.exe ([microsoft](https://learn.microsoft.com/en-us/troubleshoot/windows-server/performance/use-userdump-create-dump-file))***

_to dump processes without attaching a debugger and without affecting the process_

**·** ***BinText (mcafee)***  
**·** ***listdlls ([sysinternals](https://learn.microsoft.com/en-us/sysinternals/downloads/listdlls))***
**·** ***handle ([sysinternals](https://learn.microsoft.com/en-us/sysinternals/downloads/handle))***

_Once done with the dumping process, use debugging tools to analyze the dump files_

### ***3. RAM Acquisition***

• **RAM Capturer ([Belkasoft](https://belkasoft.com/ram-capturer))**   
• **FTK Imager ([AccessData](https://www.exterro.com/ftk-imager))**
• **dd utility (gnu.org)**

_to reliably extract the entire contents of computer’s volatile memory_

**you can read this  [medium article](https://medium.com/@lucideus/windows-volatile-memory-acquisition-forensics-2018-lucideus-forensics-3f297d0e5bfd)  for more details**

**Ps: use hash to verify the integrity of acquired data**

### ***4.***  ***Memory Forensics: Malware Analysis***

• **Redline ([fireeye](https://fireeye.market/apps/211364))**

![](https://miro.medium.com/v2/resize:fit:700/1*pfQgy5RuEZDQ-R4T3oXiEA.png)

**Redline ([fireeye](https://fireeye.market/apps/211364))**

_Redline is a very powerful tool used to identify malicious activities through memory and helps forensic investigators to establish the timeline and scope of an incident_

• **volatility & its malfind plugin ([volatilityfoundation]**(https://www.volatilityfoundation.org/releases)) 

_to analyze RAM contents and retrieve information, such as processes and executable files running in the system, open ports, IP addresses, and user login information_

_The  **malfind** plugin is used to identify hidden processes or injected code/DLLs in user mode memory_

> **Ps: we will try to provide Labs for both tools soon !**

### ***5. Virtual Memory Acquisition***

_Virtual memory, also known as logical memory, is a concept in computing that enables programmers to access a vast range of memory addresses for storing data. On Windows operating systems, virtual memory includes:_

**hiberfil.sys:**  _snapshot of the RAM data, created when hibernation is on_

**pagefile.sys:** _uses hard disk space as RAM when its out of memory_

**swapfile.sys:**  _used to store the idle and non active process data_

• **FTK Imager ([AccessData](https://www.exterro.com/ftk-imager))**

_FTK Imager can be used to traverse local system root and export these virtual memory files for analysis_

• **strings [options] file (gnu.org)**

_to pull human readable text from binary files_

**_Strings Examples_**
```
strings pagefile.sys | grep -i "^[a-z]:\\\\" | sort | uniq | less
```
_To list all the directories/path in a system_
```
strings pagefile.sys | egrep "^https?://" | sort | uniq | less
```
_To extract all the URLs recorded in the evidence file_
```
strings pagefile.sys | egrep '([[:alnum:]_.-]{1,64}+@[[:alnum:]_.-]{2,255}+?\.[[:alpha:].]{2,4})'
```

_To list all the Email Addresses in the evidence file_

