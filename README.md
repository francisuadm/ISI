## ISI (intsurg)



[Dell Performance Dock – WD19DCS](https://www.dell.com/support/home/en-us/product-support/product/dell-wd19dcs-dock/drivers)

[Dell Dock WD19/WD22 Series Firmware Update Utility](https://dl.dell.com/FOLDER08634239M/1/DellDockFirmwarePackage_WD19_WD22_HD22_Series_01.00.09.exe)

[Realtek USB GBE Ethernet Controller Driver](https://dl.dell.com/FOLDER08550499M/3/Realtek-USB-GBE-Ethernet-Controller-Driver_3K7FF_WIN_1153.6.0418.2022_A27_01.EXE)


## Poly HUB Desktop

[HUB Desktop for Windows](https://www.poly.com/content/dam/www/software/PlantronicsHubInstaller.exe)

[HUB Desktop for MAC](https://www.poly.com/content/dam/www/software/PlantronicsHubInstaller.dmg)



## Microsoft technical documentation
[URL:](https://docs.microsoft.com/en-us/)

[Open Display settings](https://support.microsoft.com/en-us/windows/view-display-settings-in-windows-37f0e05e-98a9-474c-317a-e85422daa8bb)

cut and paste to the run command: ms-settings:display?activationSource=SMC-IA-4027860

[Enable Remote Destkop](https://support.microsoft.com/en-us/windows/how-to-use-remote-desktop-5fe128d5-8fb1-7a23-3b8a-41e636865e8c)

cut and paste to the run command: ms-settings:remotedesktop?activationSource=SMC-IA-4028379


[Launch the Windows setting app via ms-setting command: ](https://docs.microsoft.com/en-us/windows/uwp/launch-resume/launch-settings-app)


## DisplayLink Graphics

[Download now](https://www.synaptics.com/products/displaylink-graphics/downloads/windows)

## How to install apps on Windows 10/11 without Microsoft Store

[Find the URL of the app](https://lazyadmin.nl/it/install-microsoft-store-apps-without-store/)

[Online link generator for Microsoft Store](https://store.rg-adguard.net/)

[Remote](https://intusurg.bomgarcloud.com/?ak=cb52218da5271f025421d8c0eba520fc)


### Simple way to get MAC Address of the PC remotely

GETMAC command

[Parameters URL: ](https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/getmac?source=recommendations)

`GetMAC /s hostname /fo table /v`


# RunAs Powershell Administrator

Use the commands below: you can save this as RunAs.PS1

```
Clear-Host
#Start -Verb RunAs -FilePath Powershell_ISE
Start-Process powershell -Credential domain\a-account -ArgumentList '-noprofile -command &{Start-Process "powershell_ise" -verb runas}'
```

If you want to make sure you are running as a-account simply type in ``` whoami```


#### [running with full privileges, in the script file.](https://superuser.com/questions/108207/how-to-run-a-powershell-script-as-administrator)

```
    $CurrentUser = New-Object Security.Principal.WindowsPrincipal $([Security.Principal.WindowsIdentity]::GetCurrent())
    $TestAdmin = $CurrentUser.IsInRole([Security.Principal.WindowsBuiltinRole]::Administrator)

If ($TestAdmin -eq $False) {
    Start-Process powershell.exe -Verb RunAs -ArgumentList ('-noprofile -noexit -file "{0}" -elevated' -f ($myinvocation.MyCommand.Definition))
exit $LASTEXITCODE
}
```

### [How to Use RunAs Without Password Prompt?](http://woshub.com/run-program-as-different-user-windows/)

You can save the user credentials (with password) that you enter. The ```/savecred``` parameter is used for this.

```runas /user:admin /savecred “C:\Windows\cmd.exe”```

After specifying the password, it will be saved to the Windows Credential Manager.

The next time you run the runas command under the same user with the ```/savecred``` key, Windows will automatically use the saved password from the Credential Manager without prompting to enter it again.

To display a list of saved credentials in Credential Manager, use the following command:

```rundll32.exe keymgr.dll, KRShowKeyMgr```


### Powershell Administrator Command


`get-pnpdevice -FriendlyName '*Poly*' | Select Stauts, Class, FriendlyName, InstanceID`

or

`get-pnpdevice -Class AudioEndpoint | Where-Object {$_.FriendlyName -like "*Poly*"} | ft status, FriendlyName, InstanceID`

`get-pnpdevice  | Where-Object {$_.Class -like "*AudioEndpoint*"} | ft status, FriendlyName, InstanceID`

`Get-WmiObject Win32_pnpEntity | Where-Object {$_.Status -like "*Poly*" | Select Status, Name, PNPDeviceID`

`Get-WmiObject Win32_pnpEntity | Where-Object {$_.Status -like "*Unknown*" | Select Status, Name, PNPDeviceID`


okay from the list
to remove it
`pnputil /remove-device 'enter InstanceID HERE'`

or you can create this via powershell
this command will capture all unknown device as AudioEndpoint

`$unknown = get-pnpdevice -Class AudioEndpoint | Where-Object {$_.Status -eq "Unknown"} | ft status, FriendlyName, InstanceID, Class`

to save it in txt file
type in
$unknown >> 1.txt

or

`Get-PNPDevice -Class AudioEndpoint | Where-Object {$_.Status -like "*Unknown*"} | Select InstanceID >> 1.txt`

To remove it

type in

`pnputil /remove-device "SWD\MMDEVAPI\{0.0.0.00000000}.{D7350DC7-645C-4E5A-85CF-9E9D19C822EA}"`

`pnputil /remove-device "SWD\MMDEVAPI\{0.0.0.00000000}.{A3107522-D577-4D7B-BF94-991D3351ED2D}"`

#### URL:
`https://social.msdn.microsoft.com/Forums/security/en-US/7834d3e9-80b7-4d6e-a76f-b6d44c7ed36b/remove-driver-with-powershell?forum=wdk`


#### How to uninstall Box Tools remotely via PowerShell

```
Open PowerShell as Administrator
PS C:\ps> runas /user:domain\a-Account powershell 
Enter
It will prompt you to enter you password.
You'll get a new PowerShell window.
PS C:\WINDOWS\system32> wmic
wmic:root\cli>/node:hostname product where "vendor like 'box%'" get name, version, vendor
/node:hostname product where name="Box Tools" Call uninstall /nointeractive
```

or

### [Run a command as an Administrator using alternate credentials](https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.management/start-process?view=powershell-7.2)

```
$cred = Get-Credential
$args = '-noprofile -command "Start-Process cmd.exe -Verb RunAs -args /k"'
Start-Process pwsh.exe -Credential $cred -WindowStyle Hidden -ArgumentList $args
```

#### How to install Box Tools remotely via Powershell

```
PS C:\ps> winrs -r:hostname powershell
PS C:\installed> curl https://e3.boxcdn.net/box-installers/boxedit/win/currentrelease/BoxToolsInstaller-AdminInstall.msi -O BoxToolsInstaller-AdminInstall.msi
PS C:\installed> .\boxtoolsinstaller-admininstall.msi
OLD info PS C:\installed> curl https://e3.boxcdn.net/box-installers/boxedit/win/currentrelease/BoxToolsInstaller.exe -O BoxToolsInstaller.exe
OLD info PS C:\installed> .\BoxToolsInstaller.exe /exenoui
PS C:\installed> get-process | where {$_.ProcessName -like "BoxTools*"} | ft *
or 
PS C:\installed> get-process -name boxtoolsinstaller
PS C:\installed> $a = get-process -name boxtoolsinstaller
PS C:\installed> $a[1].MainWindowTitle
PS C:\installed> Get-WmiObject win32_process | where {$_.ParentProcessId -eq $a.Id}
PS C:\installed> get-process | where {$_.PriorityClass -and $_.PriorityClass -ne 'Normal'} | select Name,PriorityClass,PriorityBoostEnabled
```


### *[Get all processes that have a main window title and display them in a table ](https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.management/get-process?view=powershell-7.2)*

```Get-Process | Where-Object {$_.mainWindowTitle} | Format-Table Id, Name, mainWindowtitle -AutoSize```

If you’re running PowerShell 6+ on Windows, you now have a _**ComputerName**_ parameter you can use to query processes on remote computers.

```Get-Process -ComputerName 'hostname' | Where-Object {$_.mainWindowTitle} | Format-Table Id, Name, mainWindowtitle -AutoSize```

****You can still search it by follow this command below:****

```Get-Process Outlook* ```  or  ```Get-Process | Where-Object {$_.ProcessName -like "Outlook*"}```

****To terminate the program Outlook use the command below:****

```Get-Process | Where-Object {$_.ProcessName -eq "Outlook"} | Stop-Process -Force```


#####
**Below is another great example. For each instance of the chrome process it finds, it uses that process’s ID ($_.id) and passes it to Get-NetTCPConnection. PowerShell then uses Get-NetTCPConnection to find information about each network connection the brave process has open.**

**[Run the following code in your PowerShell session when the Chrome browser is running.](https://adamtheautomator.com/powershell-get-process/)**
#####

```Get-Process -Name chrome | ForEach-Object { Get-NetTCPConnection -OwningProcess $_.Id -ErrorAction SilentlyContinue } ```


#### Force Reboot remote PC via PowerShell

```wmic:root\cli>/node:cnd14705hx os where primary="true" call reboot /nointeractive```
##

## Windows Regedit command - Changing your password to PIN:

##### Command to get your current user SID ID: whoami /user

Change Windows regedit

[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Authentication\LogonUI\UserTile](https://appuals.com/how-to-switch-login-method-from-pin-to-password/)

Now select your SID double click it, then paste this {D6886603-9D2F-4EB2-B667-1971041FA96B}

gpedit

The group policy setting you need to change can be found in the following folder: [`Computer Configuration\Administrative Templates\System\Logon`](https://serverfault.com/questions/830772/how-to-enable-pin-login-for-domain-joined-windows-10-pro-via-group-policy)

The setting you need to enable is: `Turn on convenience PIN sign-in`

Once you enable the setting, run gpupdate.exe from the command-line to refresh your the policy

##

## Remotely get the local user current printer list

Use Powershell command but only work with a-account

```
Get-CimInstance -ClassName CIM_Printer -ComputerName hostname

```
## Remotely get the local current network adapter info

```
Get-NetAdapter -CimSession [remote computername here.] -Physical | Out-GridView 
```
## BOX info

When you see this message below "Install Box Tools" to open this file on your desktop. You need to download it, by clicking the URL.
![](https://github.com/francisuadm/ISI/blob/a4d39151b927a64d47bf9cc48deaae3a866cc310/Box/BoxTools.jpg)

```
After you download the installing file, go ahead and uninstall the existing Box Tools first before you re-install it.
Make sure you are admin into the PC or else it will not work. Also make sure everything that related with Box apps is closed.
to find out open up CMD as admin, then type in
```
``tasklist /M box*``

```to terminate those apps, type in```
``taskkill /f /IM box* /t``

```
NOTE: If it continues to not allow you to open this file on your desktop. Then you'll have to uninstall all of the Box product.
After you uninstall all of the Box product, then reboot. Once you are log back in, first install Box Tools, second app is Box 
and the last is Box for Office, then reboot. All of this needs to be done locally, can't do it remotely you tried it didn't work.
```

##


## MAC OS info

Network Configuration location `/Library/Preferences/SystemConfiguration`

To rebuilt networks, delete the following files in `/Library/Preferences/SystemConfiguration/`

Note: you might not find the file called "com.apple.network.identification.plist" which is ok and, this will take at-least 15mins after reboot.

```
com.apple.airport.preferences.plist
com.apple.network.identification.plist
com.apple.wifi.message-tracer.plist
NetworkInterfaces.plist
preferences.plist
```

and ``com.apple.network.eapolclient.configuration.plist``

#### But if you just want to delete location profile just delete 

``preferences.plist and com.apple.accounts.exists.plist``

#### [Check URL for Wi-Fi Problems](https://osxdaily.com/2016/09/22/fix-wi-fi-problems-macos-sierra/)

#### [Disabling AirDrop from the command line](https://derflounder.wordpress.com/2011/10/07/disabling-airdrop-from-the-command-line/)

#### [Show logs two minutes ago,](https://blog.kandji.io/mac-logging-and-the-log-command-a-guide-for-apple-admins) ``` log show --last 2m ```

##


