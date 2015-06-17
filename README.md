# cInternetSettings

The **cInternetSettings** module contains the **cZoneSite** resource, which adds or removes sites from zones for the current user in Internet Exporer Internet Settings.

## Installation

To install **cInternetSettings** module

*   Unzip the content under $env:ProgramFiles\WindowsPowerShell\Modules folder

To confirm installation:

*   Run **Get-DSCResource** to see that **cInternetSettings** is among the DSC Resources listed.


## Requirements

This module requires the latest version of PowerShell (v4.0, which ships in Windows 8.1 or Windows Server 2012R2).
To easily use PowerShell 4.0 on older operating systems, [<span style="color:#0000ff">install WMF 4.0</span>](http://www.microsoft.com/en-us/download/details.aspx?id=40855).
Please read the installation instructions that are present on both the download page and the release notes for WMF 4.0.


## Description

The **cInternetSettings** module contains the **cZoneSite** resource, which adds or removes sites from zones for the current user in Internet Exporer Internet Settings.

Adding the FQDN of a computer to the LocalIntranet Zone will allow running programs from a share on that computer using Start-Process even if the Execution Policy is set to RemoteSigned. This is useful when installing software using DSC resources.

## Details

**cZoneSite** resource has following properties:

* **Uri:** URI to be part of the Zone.

* **Ensure** Set if Uri is present or absent.
	Valid values are:

	* Present
	* Absent

* **Type** Set type of Uri. 
	Valid values are:

	* *
	* file
	* ftp
	* http
	* https
	* knownfolder
	* ldap
	* news
	* nntp
	* oecmd
	* shell
	* snews
	
* **Zone**: Name of zone.
	Valid values are:

	* MyComputer
	* LocalIntranet
	* TrustedSite
	* Internet
	* Restricted
	
* **Platform**: Add Uri for 32-bit, 64-bit or All platforms.
	Valid values are:
	
	* x86
	* x64
	* All
	
## Versions

### 1.0.0.0

*   Initial release with the following resources 
    * cZoneSite

## Examples

Add server.contoso.com to LocalIntranet to be able to install a software from the share \\server01.contoso.com\share when Execution Policy is set to RemoteSigned.

```powershell
Configuration TrustServer01 
{
    Import-DscResource -Module cInternetSettings
    cZoneSite Source
    {
        Ensure = 'Present'
        Uri = 'server01.contoso.com'
        Type = '*'
        Zone = 'LocalIntranet'
        Platform = 'All'
    }
} 
```


