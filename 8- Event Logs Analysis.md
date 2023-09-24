# Windows Forensics: (8- Event Logs Analysis) :keyboard:

![Windows Forensics: Event Logs Analysis](https://miro.medium.com/v2/resize:fit:700/1*vNlB7On33QTQpIQZAh9ZVQ.png)

***Window Event Logs Forensics***

**We reached the eighth and final phase of Windows forensics process, all the 7 previous steps are mentioned below:**

> _1- Gathering Volatile Information:  [link](https://github.com/mazyaar/Windows_Forensic_Investigation_8_parts/blob/main/1-%20Gathering%20Volatile%20Information.md
)_
> 
> _2- Collecting Non-volatile Information:  [link](https://github.com/mazyaar/Windows_Forensic_Investigation_8_parts/blob/main/2-%20Collecting%20Non-volatile%20Information.md)_
> 
> _3- Memory Analysis:  [link](https://github.com/mazyaar/Windows_Forensic_Investigation_8_parts/blob/main/3-%20Memory%20Analysis.md)_
> 
> _4- Registry Analysis:  [link](https://github.com/mazyaar/Windows_Forensic_Investigation_8_parts/blob/main/4-%20Registry%20Analysis.md)_
> 
> _5- Cache, Cookies, and History Analysis:  [link](https://github.com/mazyaar/Windows_Forensic_Investigation_8_parts/blob/main/5-%20Examine%20the%20Cache,%20Cookies,%20and%20History%20Recorded%20in%20Web%20Browsers.md
)_
> 
> _6.7- Windows Files and Metadata analysis:  [link](https://github.com/mazyaar/Windows_Forensic_Investigation_8_parts/blob/main/6%E2%80%937-%20Examine%20Windows%20Files%20and%20Metadata.md)_

_The Windows operating system logs all user activity on the system and can serve as a valuable source of evidence in a forensic investigation. By parsing these event log files, investigators can identify indicators of malware activity, external device connections, unauthorized data access or exfiltration, and more._

## Definition

-   _On any Windows system, event logs capture a range of everyday occurrences._
-   _While some events are logged by default, others are subject to audit configurations stored in the  **PolAdEvt** registry key._
-   _Event log configuration are maintained in:_ ``HKLM\SYSTEM\CurrentControlSet\Services\Eventlog\<EventLog>``

![](https://miro.medium.com/v2/resize:fit:700/1*fKbzPKwzT_kJKcGk5CGiNQ.png)

***Event log Registry configuration***

-   _Log structure: header record(1), event records(*), end-of-file record(1)_

## Windows 10 Event Logs

_Windows 10 store event logs in ``EVTX`` file format and are based on ``XML``_
```
wevtutil el
```
to list available event logs on the system

![](https://miro.medium.com/v2/resize:fit:700/1*w4RPsxrKu38nPQ7iOUR4Ng.png)
```
wevtutil gl <log_name>
```
_to list configuration information about a specific event log_

![](https://miro.medium.com/v2/resize:fit:700/1*Pbb8GfyBpv-shh8CJmGeLA.png)

### Evaluating Account Management Events

-   _Used to record changes to accounts and group membership including: Creation, Deletion, Disabling of accounts, Modifying which accounts belong to which groups, Account lockouts, Account reactivations_

![](https://miro.medium.com/v2/resize:fit:700/1*K7v29ayYcCdcf3ceoUDk4Q.png)

-   _When a system is compromised, attackers will often attempt to disable auditing (policy change > ‘4719’ event)_

![](https://miro.medium.com/v2/resize:fit:700/1*ypiP_aKfTseCR2TIqKtBtw.png)

-   _To locate the audit policies:_  
    ``secpol.msc > Local Policies > Audit Policy > Audit Policy Change``

![](https://miro.medium.com/v2/resize:fit:700/1*ePePNq_1DlMjABrBvjq88Q.png)

## Event Logs

-   _Windows event logs are stored in: ``C:\Windows\System32\winevt\Logs``_
-   _Three main components of the Windows event logs are:_  
    **- Application Log:**  _It records the application-related events like VNC & RDP clients._  
    **- Security Log:**  _It records logon/logoff, unauthorized, and security related activities._
    **- System Log:**  _It records events related to Windows system components such as device drivers and hardware changes, starting and stopping of services, etc._
-   ***Tools such  [Microsoft Log Parser](https://www.microsoft.com/en-us/download/details.aspx?id=24659)  and  [Event Log Explorer](https://eventlogxp.com/)  can help parsing event log***
-   ***Use Filter and Find features in Event Viewer, under the Actions pane.***

![](https://miro.medium.com/v2/resize:fit:700/1*vijySIvQo4Q5xCd-lP8LvA.png)

### Examining Removable Storage Using Event Viewer

-   _Configure the Audit File System and Audit Removable Storage to enable auditing of all access requests from all removable storages_  
    ``secpol.msc > Advanced Policy Configurations > System Audit Policies > Object Accesses > Audit Removable Storage``

![](https://miro.medium.com/v2/resize:fit:700/1*GzIluLi0w9lZpvDpbFvknQ.png)

-   ***Once enabled, search for event ID 4663 where Task Category is Removable Storage***

>I hope this was helpful, See you next time
