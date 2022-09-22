## ISI



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

## How to install apps on Windows 10/11 without Microsofot Store

[Find the URL of the app](https://lazyadmin.nl/it/install-microsoft-store-apps-without-store/)

[Online link generator for Microsoft Store](https://store.rg-adguard.net/)

[Remote](https://intusurg.bomgarcloud.com/?ak=cb52218da5271f025421d8c0eba520fc)




## Powershell command


First type in
Powershell Admin command
get-pnpdevice -FriendlyName '*Poly*' | Select Stauts, Class, FriendlyName, InstanceID

or

get-pnpdevice -Class AudioEndpoint | Where-Object {$_.FriendlyName -like "*Poly*"} | ft status, FriendlyName, InstanceID

get-pnpdevice  | Where-Object {$_.Class -like "*AudioEndpoint*"} | ft status, FriendlyName, InstanceID


okay from the list
to remove it
pnputil /remove-device 'enter InstanceID HERE'

or you can create this via powershell
`this command will capture all unknown device as AudioEndpoint
`$unknown = get-pnpdevice -Class AudioEndpoint | Where-Object {$_.Status -eq "Unknown"} | ft status, FriendlyName, InstanceID, Class

to save it in txt file
type in
$unknown >> 1.txt

to remove it
type in

pnputil /remove-device "SWD\MMDEVAPI\{0.0.0.00000000}.{D7350DC7-645C-4E5A-85CF-9E9D19C822EA}"
pnputil /remove-device "SWD\MMDEVAPI\{0.0.0.00000000}.{A3107522-D577-4D7B-BF94-991D3351ED2D}"
pnputil /remove-device "SWD\MMDEVAPI\{0.0.1.00000000}.{F782537E-AB2E-40CD-85F5-A040862171A6}"
pnputil /remove-device "SWD\MMDEVAPI\{0.0.0.00000000}.{BCB3AE8F-F566-47EC-BDE1-8A9C797F3E2D}"
pnputil /remove-device "SWD\MMDEVAPI\{0.0.1.00000000}.{5B7E4F92-F813-4F41-88C0-FC9BBA6FB5DB}"
pnputil /remove-device "SWD\MMDEVAPI\{0.0.1.00000000}.{4CE42858-082B-4444-8C16-BB8529359719}"
pnputil /remove-device "SWD\MMDEVAPI\{0.0.1.00000000}.{EA1C87A5-D417-4C86-BB4B-0F58E61213A1}"
pnputil /remove-device "SWD\MMDEVAPI\{0.0.0.00000000}.{63134EE0-B6F1-4CEB-A1C3-CEAA25BF8A9D}"

you found this from this URL:
https://social.msdn.microsoft.com/Forums/security/en-US/7834d3e9-80b7-4d6e-a76f-b6d44c7ed36b/remove-driver-with-powershell?forum=wdk

