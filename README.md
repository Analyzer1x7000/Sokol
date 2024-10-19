![image](https://github.com/Analyzer1x7000/Sokol/assets/103800652/0565b017-9211-4a1f-91ab-97a03677fa3e)


# About Sokol
Sokol is a PowerShell script designed to be used via CrowdStrike RTR as a `CloudFile`. Similar to KAPE, it pulls critical forensic artifacts from a target during IR, so that the artifacts can be analyzed on a separate forensic workstation.

Sokol contains several modules that can be run individually, or all at once.

## Setup
Create a new script via `Configuration` -> `Response Scripts & Files` and name it "Sokol"

![image](https://github.com/Analyzer1x7000/Sokol/assets/103800652/b0b05280-712d-4aaa-bd32-8f8842a13691)

## Running Sokol from CrowdStrike RTR Console

To run Sokol from the CrowdStrike RTR console:
```
  runscript -CloudFile='Sokol' -CommandLine='-module all'
  OR 
  runscript -CloudFile='Sokol' -CommandLine='-module Services'
```

## Running Sokol Directly w/ Powershell

- Set execution policy to Unrestricted under the scope of the current process

`Set-ExecutionPolicy Unrestricted -Scope Process`

- Run Sokol.ps1 with the appropriate parameter(s)

`.\Sokol.ps1 -module all`

## Features
```
PARAMETERS
  -module all           : run all modules
  -module <name>        : run specific module
  -folder <path>        : output folder [Default: C:\Windows\Temp\IR]
  -module help          : display usage

MODULES
  {Malware - Persistence}
    AutoRuns              : Gather files in common startup locations
    Services              : Gather Windows Services
    InstalledSoftware     : Gather Installed Software from Uninstall Key
    DNSCache              : Get clients local DNS cache
    RunningProcesses      : Get all running processes and hashes
  
  {Forensics - Evidence of Execution}
    Prefetch              : Get list of files in prefetch
    PEFiles               : Get list of PE files and hashes in user writeable locations
    JumpLists             : Get a copy of JumpLists (AutomaticDestinations & CustomDestinations)
    SRUM                  : Get a copy of SRUDB.DAT
  
  {Forensics - Deleted Items & File Existence}
    RecycleBin            : Get a copy of the contents of $Recycle.Bin
    Thumbcache            : Get a copy of the Thumbcache from user's %AppData% folder
    WordWheelQuery        : Get a copy of WordWheelQuery key from NTUSER.DAT hive
    UserTypedPaths        : Get a copy of TypedPaths from NTUSER.DAT hive
  
  {Forensics - Files & Folders Opened}
    LNKFiles              : Get LNK files on desktop and recent files list
    OpenSaveMRU           : Get a copy of OpenSavePidlMRU from NTUSER.DAT hive
    OfficeRecentfiles     : Get Office file MRU lists from NTUSER.DAT hive
  
  {Malware - Miscellaneous}
    OfficeFiles           : Get list of office docs and hashes in user writeable locations
    ScriptFiles           : Get list of scripts and hashes in user writeable locations
  
  {Forensics - Miscellaneous}
    EventLogs             : Gather Event Logs
    HiddenFilesDirs       : Get hidden files and directories
    WindowsUpdates        : Get installed windows updates
    BrowserExtensions     : Get list of extensions for Chrome and Firefox
    KrbSessions           : Get list of kerberos sessions
    Recall                : Gathers screenshots and other data from Microsoft's Recall feature  
```

