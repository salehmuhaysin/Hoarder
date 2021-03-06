# Hoarder
This script is made to collect the most valuable artifacts for forensics or incident response investigation rather than imaging the whole hard drive.

## Executable Releases:
You may find the executable binaries for x86 and x64 on 
>> will be added soon

## Installing Dependences

To install Hoarder  dependences run the following command on a privileged terminal:

`pip install -r requirment.txt` 

## Usage

Make sure that `Hoarder.yml` is on the same directory as the script. `Hoarder.yml` is YAML file that contains artifacts. Hoarder will read this file and generate argument at runtime (try `python hoarder.py -h`). The following is the list of argument :

```
usage: hoarder.py [-h] [-V] [-v] [-vv] [-a] [-p] [-s] [--PowerShellHistory]
                  [--Config] [--SystemInfo] [--CCM] [--WMITraceLogs]
                  [--Firwall] [--Events] [--usrclass] [--BMC] [--Ntuser]
                  [--WERFiles] [--SRUM] [--Jump_List] [--Recent] [--Ntfs]
                  [--applications] [--WMI] [--scheduled_task] [--Startup]
                  [--BrowserHistory] [--prefetch] [--RecycleBin]
                  [--WindowsIndexSearch]

Hoarder is a tool to collect windows artifacts.

optional arguments:
  -h, --help            show this help message and exit
  -V, --version         Print Hoarder version number.
  -v, --verbose         Print details of hoarder message in console.
  -vv, --very_verbose   Print more details (DEBUG) of hoarder message in
                        console.
  -a, --all             Get all (Default)

Plugins:
  -p, --processes       Collect information about the running processes.
  -s, --services        Collect information about the system services.

Artifacts:
  --PowerShellHistory   PowerShell history for all the users
  --Config              System hives
  --CCM                 CCM Logs
  --WMITraceLogs        WMI Trace Logs
  --Firwall             Firewall Logs
  --Events              Windows event logs
  --usrclass            UserClass.dat file for all the users
  --BMC                 BMC files for all the users
  --Ntuser              All users hives
  --WERFiles            Windows Error Reporting Files
  --SRUM                SRUM folder
  --Jump_List           JumpList files
  --Recent              Recently opened files
  --Ntfs                $MFT file
  --applications        Amcache files
  --WMI                 WMI OBJECTS.DATA file
  --scheduled_task      Scheduled Tasks files
  --Startup             Startup info
  --BrowserHistory      BrowserHistory Data
  --prefetch            Prefetch files
  --RecycleBin          RecycleBin Files
  --WindowsIndexSearch  Windows Search artifacts

Commandss:
  --SystemInfo          Get system information


```

#### Plugins vs Commands:
- **Plugins**: predefined functions inside the script can be called to get specific results, such as processes and services
- **Commands**: defined inside `Hoarder.yml` to execute single command-line, such as `systeminfo`


#### Example

Let's say you want to collect all of the artifacts specified in `Hoarder.yml` then all you need to do is:

`python hoarder.py --all` or `python hoarder.py -a` 

After the script finishes it will generate a zip file called `<HOSTNAME>.zip` contains all of the artifacts in addition to  `hoarder.log` that contains the script debugging logs.


## Add an Artifact to Hoarder.yml

### File and Folder Artifacts

The following is an example for file or folder collection:

```yaml
  applications: 
      output: 'applications'
      path32: '\Windows\AppCompat\Programs\'
      path64: '\Windows\AppCompat\Programs\'
      files:  
      - Amcache.hve*
      - RecentFileCache.bcf
      description: 'Amcache files'
```

* **applications** : This is the name of the artifact. This name will be used as an argument in the hoarder command line.
* **output** : This is the name of the output folder for this artifact.
* **path32** : The path to the artifact for 32bit systems, you can use \* as widecard, and ** as recursive.
* **path64** : The path to the artifact for 64bit systems, you can use \* as widecard, and ** as recursive.
* **files** : The file name/s. it could be a single string or a list as the example above, also you can use * as widecard.
* **description** : a description about the artifact. This key is used in hoarder command line to show some information about the artifact.

### Command Execution 

Hoarder also support the execution of system commands. The following example shows the execution of the command "systeminfo":

```yaml
  SystemInfo:
    output: 'SystemInfo'
    cmd: 'systeminfo'
    description: 'Get system information'
```

* **SystemInfo** : This is the name of the artifact. This name will be used as an argument in the hoarder command line.

* **output** : This is the name of the output folder for this artifact.

* **cmd** : The command to be executed.

* **description** : a description  about the artifact. This key is used in hoarder command line to show some information about the artifact.

## Contributors:
Big thanks to [AbdulRhman Alfaifi](https://github.com/AbdulRhmanAlfaifi) and [Saleh Bin Muhaysin](https://github.com/salehmuhaysin) for their tremendous effrot in rewriting this project in a proper way and his ideas.
