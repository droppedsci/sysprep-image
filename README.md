# sysprep-image

Steps for sysprep on Windows 10 1607
Download the latest ADK version. Below is the link :
https://developer.microsoft.com/en-us/windows/hardware/windows-assessment-deployment-kit

Run the Windows 10 Installation

Disable first sign-on animation(optional)
Open Group Policy Editor

Local Computer Policy->Computer Configuration->Administrative Templates->System->Logon->Show First sign-in animation->Disable

Login with an account within the Administrator Group or with Domain Administrator privileges. 

Other settings: Enable Administrator if necessary. Add network printers

To activate the inactive administrator account, run the command net user administrator /active:yes
If you want to enable the guest account as well run the command net user guest /active:yes
Launch a POWERSHELL as an ADMIN and run Get-AppxPackage -AllUsers | Remove-AppxPackage

Remove local Administrator password. 

Go to c:\windows\System32\sysprep\sysprep.exe
Select in the dropdown box 'audit', Click on 'Generalize' and then 'Reboot'.

After system reboots, it will login as Administrator and you will not be prompted for a password if you removed the password correctly. 

After booting is complete,remove all the user profiles except Administrator and Default. They can be found in control panel/user profiles

Then go to 'This PC', click 'Manage' and find 'Local Users and Groups. Delete all groups and users except for Administrator and guest.

Run Disk Cleanup or CC cleaner

Download Updates

Hi. I am trying to create a value in the default user profile runonce to point at a login script.
This means that when you create a new user profile, the runonce script will execute when the user first logs in.
As far as I am aware, this process can not be done by script, but only manually, like this.
01) open regedit
02) go to HKEY_USERS
03) Load Hive
04) Browse to C:\Documents and Settings\Default User\ntuser.dat
05) give it a temporary key name, for example ZZZ
06) go to HKEY_USERS\ZZZ\Software\Microsoft\Windows\CurrentVersion
07) Create a key RunOnce
08) Create a string value there eg: First Run, then change the value to where your script sits, eg: "D:\User\zxp\newUserProfile.cmd"
09) go back to HKEY_USERS\ZZZ
10) unload the hive
Now when you create a new user, the runonce value runs on the first login so you can run a first time user script; eg newUserProfile.cmd



Download and unzip THIS simple unattend file for you SYSPREP or make your own using WAIK
Copy the UNATTEND.XML to your C:\
Open a CMD PROMPT as an Administrator
CD into the C:\WINDOWS\SYSTEM32\SYSPREP folder
Paste in this command
sysprep /oobe /generalize /shutdown /unattend:C:\windows\setup\scripts\unattend.xml

Power the machine up when it is done, PXE boot off the network and push the image to your Windows Deployment Services WDS server

Second part of sysprep - Capture the image 

Power down PC
Turn on PC and halt boot process. Do not boot to local drive. Boot to a WinPE boot disk

at prompt type diskpart




