## Determine whether the Hyper-V hypervisor is running

[Source](https://learn.microsoft.com/en-us/troubleshoot/windows-client/application-management/virtualization-apps-not-work-with-hyper-v)

To determine whether the Hyper-V hypervisor is running, follow these steps:

1. In the search box, type _msinfo32.exe_.
    
2. Select **System Information**.
    
3. In the detail window, locate the following entry:
    
    > A hypervisor has been detected. Features required for Hyper-V will not be displayed.

---
## [Source 1 :](https://allthings.how/how-to-disable-hyper-v-in-windows-11/) 

### Disable Hyper-V From Windows Features

The Optional Features (a.k.a "Windows Features") tool allows you to add additional features that don't come preinstalled in Windows 11. Similarly, it can also help you disable those advanced features.

1. Open the Start Menu and type 'Control Panel' in search box. Click on 'Control Panel' from the search results.
2. Select the 'Programs & features' option on the Control Panel window.

![](https://allthings.how/content/images/2023/12/image-579.png)

3. Click on 'Programs & features' from the right section of the window. If you have the 'Category' view of the Control Panel, select the 'Programs' option.

![](https://allthings.how/content/images/2023/12/image-580.png)

4. On the subsequent screen, select 'Turn Windows features on or off'. A new window will open on your screen.

![](https://allthings.how/content/images/2023/12/image-582.png)

5. On the opened window, locate and uncheck the 'Hyper-V' option.

![](https://allthings.how/content/images/2023/12/image-583.png)

6. Similarly, locate and uncheck the 'Virtual Machine Platform' and 'Windows Hypervisor Platform' and click 'OK' to save the changes.

![](https://allthings.how/content/images/2023/12/image-585.png)

7. Restart your PC from the Start Menu to apply the changes.

### Uninstall Hyper-V Using Windows Terminal

1. Open the Start Menu and type 'Terminal'. From the search results, right-click on the 'Terminal' option and select 'Run as administrator'.

![](https://allthings.how/content/images/2023/12/image-586.png)

2. A UAC (User Account Control) window will appear on your screen. Click on 'Yes' to proceed. If you are not logged in with an admin account, enter the credentials for one.
3. You can perform the function with PowerShell and Command Prompt. To disable Hyper-V with PowerShell, type or copy and paste the below-mentioned command.

```
Disable-WindowsOptionalFeature -Online -FeatureName Microsoft-Hyper-V-All
```

![](https://allthings.how/content/images/2023/12/image-587.png)

4. The process may take a few minutes to complete. Once completed, exit the Terminal and restart your PC to let the changes take effect.

#### Disable Hyper-V Using Command Prompt:

1. On the Terminal window, click on the chevron (downward arrow) and select the 'Command Prompt' option.

![](https://allthings.how/content/images/2023/12/image-588.png)

2. Type or copy and paste the below-mentioned command and hit `Enter` to execute it.

```
dism /online /disable-feature /featurename:Microsoft-hyper-v-all
```

![](https://allthings.how/content/images/2023/12/image-2-1.png)

3. Once executed, the Command Prompt will show a 'completed successfully' message.
4. Exit the Windows Terminal and restart your PC to apply the changes.

### Disable Hyper-V Using BCDEdit Tool

BCDEdit (Boot Configuration Data Edit) is a command-line tool that allows you to disable Hyper-V. This method can come in handy when do not wish to uninstall Hyper-V completely from your computer.

1. Open the Start Menu and search for 'Windows Terminal'. From the results, right-click on 'Windows Terminal' and select 'Run as administrator'.
2. On the Terminal window, click on the chevron (downward arrow) and select 'Command Prompt'.

![upload in progress, 0](https://allthings.how/content/images/2023/12/image-588-1.png)

3. Type or copy and paste the below-mentioned command and hit `Enter` to execute.

```
bcdedit /set hypervisorlaunchtype off
```

![](https://allthings.how/content/images/2023/12/image-3-1.png)

4. Once Hyper-V is disabled, the Command Prompt will display the success message. Exit the Terminal and restart your PC to let the changes take effect.
5. **If you wish to re-enable the Hyper-V on your computer**, type or copy and paste the below-mentioned command in an elevated Command Prompt window.

```
bcdedit /set hypervisorlaunchtype auto
```

![](https://allthings.how/content/images/2023/12/image-6-1.png)

### Disable Memory Integrity Using Windows Security

Many times, users encounter 'Hyper-V' detected issues even after uninstalling Hyper-V from their computer. To address this issue, simply disable Memory Integrity from Windows Security.

The issue typically arises when you are trying to install third-party virtualization tools. Since the 'Memory Integrity' feature is designed to restrict access to programs at the kernel level, when enabled, it will not grant any third-party tool access to the system's virtualization hardware.

1. Open the Start Menu and type 'Security'. From the search results, click on the 'Windows Security' option.

![](https://allthings.how/content/images/2023/12/image-7-1.png)

2. On the Windows Security window, click on the 'Device Security' option from the left sidebar.

![](https://allthings.how/content/images/2023/12/image-8-1.png)

3. On the subsequent screen, click on the 'Core isolation details' option.

![](https://allthings.how/content/images/2023/12/image-10-1.png)

4. Finally, turn off the toggle for the 'Memory Integrity' option.

![](https://allthings.how/content/images/2023/12/image-9-1.png)

5. Restart your PC to let the changes take effect. Once Memory Integrity is disabled, you should be able to install third-party virtualization tools.

### Uninstall Hyper-V Virtual Adapter

Not all, but some users also encountered the alert message 'We couldn't complete the updates, undoing changes', after they uninstall Hyper-V from their computer. This issue could arise due to the virtual network adapters that were not deleted during the uninstallation of Hyper-V.

1. Open the Start Menu and search for 'Device Manager'. From the search results, click on the 'Device Manager' option.

![](https://allthings.how/content/images/2023/12/image-11-1.png)

2. Click on the 'View' tab and select 'Show hidden devices' on the Device Manager window.

![](https://allthings.how/content/images/2023/12/image-12-1.png)

3. Expand the 'Network Adapters' section. Next, right-click on the 'Hyper-V Virtual Ethernet Adapter' and select the 'Uninstall device' option.

****Note:**** Do not accidentally uninstall the 'Microsoft Wi-Fi Direct Virtual Adapter' as it facilitates the Wi-Fi Direct functionality on the computer.

![](https://allthings.how/content/images/2023/12/image-13-1.png)

4. If there is more than one virtual adapter installed, delete all of them by repeating the steps above.
5. Once all adapters have been deleted, exit the Device Manager and restart your PC.

### Disable Device Gaurd and Credential Gaurd

Users typically working with VMware Workstation encounter an issue saying 'Device Gaurd/Credential Gaurd' is enabled when trying to power on the VMware Workstation. That being said, you can easily disable it using the Registry Editor.

Device Gaurd hardens your system and prevents malicious code from running on it. A Credential Device is another feature that isolates system and user secrets against a system compromise.

1. Open the Start Menu and search for 'Registry'. From the search results, click on the 'Registry Editor'.

![](https://allthings.how/content/images/2023/12/image-73-1.png)

2. Type or copy and paste the below-mentioned address in the address bar and hit `Enter` to navigate to it.

```
HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Lsa
```

![](https://allthings.how/content/images/2023/12/image-74-1.png)

3. On the right section of the window, double-click on the 'LsaCfgFlags'. This will open its properties.

![](https://allthings.how/content/images/2023/12/image-75-1.png)

4. If no such DWORD file exists, right-click on the empty space and hover over the 'New' option. Then, select the 'DWORD' option. Finally, rename the file to 'LsaCfgFlags'.

![](https://allthings.how/content/images/2023/12/image-76-1.png)

5. On the 'LsaCfgFlags' properties window, enter `0` in the 'Value data' field.

![](https://allthings.how/content/images/2023/12/image-77-1.png)

6. Type or copy and paste the below-mentioned address in the address bar and press `Enter` to navigate to it.

```
HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\DeviceGuard
```

![](https://allthings.how/content/images/2023/12/image-78-1.png)

7. On the right section of the window, double-click on the 'EnableVirtualizationBasedSecurity' to open its properties.

![](https://allthings.how/content/images/2023/12/image-79-1.png)

8. Type `0` in the 'Value Data' field and click 'OK' to save the changes.

![](https://allthings.how/content/images/2023/12/image-80-1.png)

9. Restart your computer to apply the changes. You should no longer experience the 'Device Gaurd and Credential Gaurd is enabled' issue on your computer. If you wish to enable them in the future, just change the value to `1` in the Registry Editor following the same steps mentioned above.

---
## [Source 2 :](https://helpdeskgeek.com/how-to-disable-hyper-v-in-windows-11/) 

### How to Disable Hyper-V

Below, we’ll explain how to remove Hyper-V using Windows Features, BCDEdit, command line, and [PowerShell](https://helpdeskgeek.com/using-powershell-for-home-users-a-beginners-guide/). Keep in mind that once removed, you’ll be unable to access Hyper-V Manager or change any VM settings until you reinstall it.

#### 1. How to Disable Hyper-V Using Windows Optional Features

The easiest way to disable Hyper-V is by using the Windows Features app. To do so:

1. Press Win + R to open Run.
2. Type control and press Enter to open the Control Panel.

[![How to Disable Hyper-V in Windows 11 image 4](https://helpdeskgeek.com/wp-content/pictures/2024/02/how-to-disable-hyper-v-in-windows-11-4-compressed.png "how-to-disable-hyper-v-in-windows-11-4-compressed - Help Desk Geek")](https://helpdeskgeek.com/wp-content/pictures/2024/02/how-to-disable-hyper-v-in-windows-11-4-compressed.png)

3. Select Programs.

[![How to Disable Hyper-V in Windows 11 image 5](https://helpdeskgeek.com/wp-content/pictures/2024/02/how-to-disable-hyper-v-in-windows-11-5-compressed.png "how-to-disable-hyper-v-in-windows-11-5-compressed - Help Desk Geek")](https://helpdeskgeek.com/wp-content/pictures/2024/02/how-to-disable-hyper-v-in-windows-11-5-compressed.png)

4. Choose Programs and Features.

[![How to Disable Hyper-V in Windows 11 image 6](https://helpdeskgeek.com/wp-content/pictures/2024/02/how-to-disable-hyper-v-in-windows-11-6-compressed.png "how-to-disable-hyper-v-in-windows-11-6-compressed - Help Desk Geek")](https://helpdeskgeek.com/wp-content/pictures/2024/02/how-to-disable-hyper-v-in-windows-11-6-compressed.png)

5. Select Turn Windows features on or off in the left-hand menu.
6. Scroll down and uncheck the checkbox next to Hyper-V, Windows Hypervisor Platform, and Virtual Machine Platform.

[![How to Disable Hyper-V in Windows 11 image 7](https://helpdeskgeek.com/wp-content/pictures/2024/02/how-to-disable-hyper-v-in-windows-11-7-compressed.png "how-to-disable-hyper-v-in-windows-11-7-compressed - Help Desk Geek")](https://helpdeskgeek.com/wp-content/pictures/2024/02/how-to-disable-hyper-v-in-windows-11-7-compressed.png)

7. Reboot your PC.

Note: This method will completely uninstall Hyper-V, meaning that if you want to use it in the future, you’ll have to reinstall it. We’ll explain how to do so below.

#### 2. How to Disable Hyper-V Using BCDEDIT

The BCDEDIT tool lets you disable Hyper-V in your PC’s boot configuration rather than uninstalling it entirely. This is useful if you want to avoid having to install Hyper-V again in the future.

To disable Hyper-V using BCDEDIT:

1. Open the Start Menu and search for “cmd.”
2. Right-click Command Prompt and press Run as Administrator.

[![How to Disable Hyper-V in Windows 11 image 8](https://helpdeskgeek.com/wp-content/pictures/2024/02/how-to-disable-hyper-v-in-windows-11-8-compressed.png "how-to-disable-hyper-v-in-windows-11-8-compressed - Help Desk Geek")](https://helpdeskgeek.com/wp-content/pictures/2024/02/how-to-disable-hyper-v-in-windows-11-8-compressed.png)

3. In the Command Prompt window, enter the following command:

bcdedit /set hypervisorlaunchtype off

[![How to Disable Hyper-V in Windows 11 image 9](https://helpdeskgeek.com/wp-content/pictures/2024/02/how-to-disable-hyper-v-in-windows-11-9-compressed.png "how-to-disable-hyper-v-in-windows-11-9-compressed - Help Desk Geek")](https://helpdeskgeek.com/wp-content/pictures/2024/02/how-to-disable-hyper-v-in-windows-11-9-compressed.png)

1. You should receive a message saying that the command was successful. When you do, restart your PC to ensure that Hyper-V is disabled.

If you ever need to re-enable Hyper-V, type the following command into Command Prompt as above:

bcdedit /set hypervisorlaunchtype auto

Then restart your PC to confirm the changes.

#### 3. How to Disable Hyper-V Using Command Prompt

If you’re unable to use the Windows Features tool to disable Hyper-V, you can uninstall it using Command Prompt. To do so:

1. Open the Start Menu and search for “cmd.”
2. Right-click Command Prompt and press Run as Administrator.
3. Type the following command and press Enter:

dism /online /disable-feature /featurename:Microsoft-hyper-v-all

1. You should receive a completion message stating that the DISM tool has disabled Hyper-V.

[![How to Disable Hyper-V in Windows 11 image 10](https://helpdeskgeek.com/wp-content/pictures/2024/02/how-to-disable-hyper-v-in-windows-11-10-compressed.png "how-to-disable-hyper-v-in-windows-11-10-compressed - Help Desk Geek")](https://helpdeskgeek.com/wp-content/pictures/2024/02/how-to-disable-hyper-v-in-windows-11-10-compressed.png)

2. Restart your PC.

#### 4. How to Disable Hyper-V Using Windows PowerShell

One final method to disable Hyper-V is by using PowerShell in admin mode. To do so:

1. Open the Start Menu and type “PowerShell.”
2. Right-click PowerShell and select Run as administrator.

[![How to Disable Hyper-V in Windows 11 image 11](https://helpdeskgeek.com/wp-content/pictures/2024/02/how-to-disable-hyper-v-in-windows-11-11-compressed.png "how-to-disable-hyper-v-in-windows-11-11-compressed - Help Desk Geek")](https://helpdeskgeek.com/wp-content/pictures/2024/02/how-to-disable-hyper-v-in-windows-11-11-compressed.png)

3. Enter the following command and press Enter:

Disable-WindowsOptionalFeature -Online -FeatureName Microsoft-Hyper-V-All

[![How to Disable Hyper-V in Windows 11 image 12](https://helpdeskgeek.com/wp-content/pictures/2024/02/how-to-disable-hyper-v-in-windows-11-12-compressed.png "how-to-disable-hyper-v-in-windows-11-12-compressed - Help Desk Geek")](https://helpdeskgeek.com/wp-content/pictures/2024/02/how-to-disable-hyper-v-in-windows-11-12-compressed.png)

1. Wait for a success message, then restart your PC to confirm the changes.

### How to Fix “We Couldn’t Complete the Updates” Error

While uninstalling Hyper-V, many users encounter an error message that states, “We couldn’t complete the updates, undoing changes.” This error prevents you from uninstalling Hyper-V and means that the original error is still going to occur.

To fix this, you need to remove the Hyper-V Virtual Network Adapter:

1. Open the Run dialog box.
2. Type devmgmt.msc and press Enter.

[![How to Disable Hyper-V in Windows 11 image 13](https://helpdeskgeek.com/wp-content/pictures/2024/02/how-to-disable-hyper-v-in-windows-11-13-compressed.png "how-to-disable-hyper-v-in-windows-11-13-compressed - Help Desk Geek")](https://helpdeskgeek.com/wp-content/pictures/2024/02/how-to-disable-hyper-v-in-windows-11-13-compressed.png)

3. In the Device Manager, double-click Network Adapters to expand the section.

[![How to Disable Hyper-V in Windows 11 image 14](https://helpdeskgeek.com/wp-content/pictures/2024/02/how-to-disable-hyper-v-in-windows-11-14-compressed.png "how-to-disable-hyper-v-in-windows-11-14-compressed - Help Desk Geek")](https://helpdeskgeek.com/wp-content/pictures/2024/02/how-to-disable-hyper-v-in-windows-11-14-compressed.png)

4. Locate Hyper-V network adapters. Select the View menu option at the top of the window, and select Show hidden devices.
5. Right-click Hyper-V Virtual Ethernet Adapter and select Uninstall Device.
6. Repeat this for every network adapter in the list. Then, reboot your PC and check if it worked on startup.

### Still Having Problems With Hyper-V? Try These Fixes

Unfortunately, you may still have issues with games and other virtualization software after removing Hyper-V. This is due to a few similar Windows features that cause conflicts with third-party virtualization tools.

Here are two things to try:

#### 1. Turn Off Memory Integrity

The memory integrity feature, found in Windows Security, helps prevent malware from infecting the most important system processes. However, it also stops certain third-party tools from being able to access key resources they need to function.

To turn off memory integrity:

1. Press the Windows key + I to open Settings.
2. Select Privacy & security.

[![How to Disable Hyper-V in Windows 11 image 15](https://helpdeskgeek.com/wp-content/pictures/2024/02/how-to-disable-hyper-v-in-windows-11-15-compressed.jpg "how-to-disable-hyper-v-in-windows-11-15-compressed - Help Desk Geek")](https://helpdeskgeek.com/wp-content/pictures/2024/02/how-to-disable-hyper-v-in-windows-11-15-compressed.jpg)

3. Choose Windows Security and select Device security.
4. Select Core isolation details.

[![How to Disable Hyper-V in Windows 11 image 16](https://helpdeskgeek.com/wp-content/pictures/2024/02/how-to-disable-hyper-v-in-windows-11-16-compressed.png "how-to-disable-hyper-v-in-windows-11-16-compressed - Help Desk Geek")](https://helpdeskgeek.com/wp-content/pictures/2024/02/how-to-disable-hyper-v-in-windows-11-16-compressed.png)

5. Toggle off Memory integrity and restart your computer.

[![How to Disable Hyper-V in Windows 11 image 17](https://helpdeskgeek.com/wp-content/pictures/2024/02/how-to-disable-hyper-v-in-windows-11-17-compressed.png "how-to-disable-hyper-v-in-windows-11-17-compressed - Help Desk Geek")](https://helpdeskgeek.com/wp-content/pictures/2024/02/how-to-disable-hyper-v-in-windows-11-17-compressed.png)

#### 2. Disable Device Guard and Credential Guard

Device Guard and Credential Guard are two Windows features that require Hyper-V to function. Due to this, there may be a [group policy](https://helpdeskgeek.com/what-is-the-windows-10-group-policy-editor/) function or [BIOS/UEFI settings](https://helpdeskgeek.com/how-to-enter-the-bios-in-windows-11/) that automatically enable Hyper-V whenever you boot up your PC.

To fix this, you need to alter the Windows registry. Modifying the registry can be risky, so we recommend creating a system restore point before performing the next steps.

Here’s how to disable Device Guard and Credential Guard:

1. Press Win + R to open Run.
2. Type Regedit and press Enter.

[![How to Disable Hyper-V in Windows 11 image 18](https://helpdeskgeek.com/wp-content/pictures/2024/02/how-to-disable-hyper-v-in-windows-11-18-compressed.png "how-to-disable-hyper-v-in-windows-11-18-compressed - Help Desk Geek")](https://helpdeskgeek.com/wp-content/pictures/2024/02/how-to-disable-hyper-v-in-windows-11-18-compressed.png)

3. Navigate to Computer\HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Lsa. You can simply copy and paste that location into the address bar at the top of the Registry Editor window.
4. Select the Lsa folder.

[![How to Disable Hyper-V in Windows 11 image 19](https://helpdeskgeek.com/wp-content/pictures/2024/02/how-to-disable-hyper-v-in-windows-11-19-compressed.png "how-to-disable-hyper-v-in-windows-11-19-compressed - Help Desk Geek")](https://helpdeskgeek.com/wp-content/pictures/2024/02/how-to-disable-hyper-v-in-windows-11-19-compressed.png)

5. In the right-hand window pane, locate LsaCfgFlags. If it doesn’t exist, right-click in the window, select New > DWORD (32-bit) Value, and name it “LsaC gFlags.”
6. Double-click the LsaCfgFlags DWORD and change the Value data field to 0.

[![How to Disable Hyper-V in Windows 11 image 20](https://helpdeskgeek.com/wp-content/pictures/2024/02/how-to-disable-hyper-v-in-windows-11-20-compressed.png "how-to-disable-hyper-v-in-windows-11-20-compressed - Help Desk Geek")](https://helpdeskgeek.com/wp-content/pictures/2024/02/how-to-disable-hyper-v-in-windows-11-20-compressed.png)

7. Select OK.
8. Now, navigate to Computer\HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\DeviceGuard.
9. Locate the EnableVirtualizationBasedSecurity DWORD value. If it doesn’t exist, create it as above.

[![How to Disable Hyper-V in Windows 11 image 21](https://helpdeskgeek.com/wp-content/pictures/2024/02/how-to-disable-hyper-v-in-windows-11-21-compressed.png "how-to-disable-hyper-v-in-windows-11-21-compressed - Help Desk Geek")](https://helpdeskgeek.com/wp-content/pictures/2024/02/how-to-disable-hyper-v-in-windows-11-21-compressed.png)

10. Double-click the DWORD and set its value to 0.
11. Select OK, then restart your computer to make sure the changes are applied.

Note: If you ever need to re-enable Device Guard or Credential Guard, repeat the steps above but set the value to 1.

---

## [Source 3 :](https://community.broadcom.com/vmware-cloud-foundation/discussion/disabling-hyper-v-hypervisor-on-windows-11-pro-host-to-get-vmware-17s-cpl0-vs-ulm-monitor-mode) 

**Phase 3:**

There is a manual way to do this, and I found the instructions, but they're a bit scary. It involves using bcdedit to modify the boot configuration to apply a configuration change that sets a "DISABLE-LSA-ISO" option. Lots of opportunity for something to go wrong if the instructions I found are flawed, or if a mistake is made (typo, missed a command). So, I'm strongly recommending (and providing instructions for) the method that uses the Microsoft-provided script. I've tested it, it worked for me, and the same script provides a way to undo the whole thing later if desired, too. Power users are welcome to find the instructions I found on their own, or to simply open the script file and examine what it does for any manual implementation activities.

1. Go to [Download Device Guard and Credential Guard hardware readiness tool](https://www.microsoft.com/en-us/download/details.aspx?id=53337), provided by Microsoft to check Device Guard and Credential Guard capability, and to turn on/off the features. There's no setting anywhere in Settings app or control panel for this, and this "tool" is actually a PowerShell script, but it provides the necessary functionality. Find the Download button and click it, and your browser will download a ZIP archive.
2. Find and extract the folder contained in the archive. Don't try to run the script from within the archive. If you're using Windows Explorer, it can make a ZIP archive look like just another folder, but it isn't. You need to drag out the "dgreadiness_v3.6" (version as of when I wrote this post) folder from the archive into a real folder, e.g. onto your Desktop.
3. Search for "**powershell**" in Start menu to find **Windows PowerShell**, right-click it, and run as administrator (elevated). You must run it elevated or the script won't work.
4. You need to change the current drive and directory to the one where the script is. If you're not command prompt savvy: type "C:" for example (no quotes) if the folder is on the C: drive, or "D:" if it's on the drive, etc., and hit Enter, which should change the active drive to the correct one; next, open the folder you extracted the script files into, copy the address from the address bar into the clipboard (highlight and Ctrl-C), then type the following command (replacing *PATH* with a Ctrl-V to paste the path you just copied), and hit Enter:  
    **cd "_PATH_"**
5. The prompt in front of your blinking cursor should now match the folder where the script file is located, meaning your "current directory" is the correct one.
6. Unless you know that you've already set this policy (power user), run this command next, to allow the script to be run:  
    **Set-ExecutionPolicy Unrestricted**
7. You'll have to respond to a security prompt by typing "y" (if I remember correctly), possibly followed by Enter. It should then say it has successfully changed the execution policy.
8. Now we can run the script. Type/paste (if the version number has changed since I posted this, adjust according to the filename of the .ps1 script file in the extracted folder):  
    DG_Readiness_Tool_v3.6.ps1 -Disable
9. The script will do some stuff, and then you'll get to restart, and during restart you will get a full-screen prompt asking you to confirm you want to opt out of Device Guard and Credential Guard. Answer in the affirmative. I don't have precise instructions for the exact sequence of events and prompts/actions after running the script, because I ran it several days ago and didn't document what I saw.
10. Once Windows has restarted with these features "opted out of," fire up System Information and check that VBS value again. For me, this was the final step that did the job, and when I ran a VMWare Workstation VM, it gave me the coveted Monitor Mode value of "CPL0"!
11. By the way, for the sake of security, you might want to change the PowerShell script execution policy back to the more restrictive default one after these steps. If so, launch **Windows PowerShell** again, as administrator, and execute:  
    **Set-ExecutionPolicy Default**

--- 
## Trouble Shooting :

### If you don't have : Hyper-V on Windows Features ?

[Source (**Fun-Group-8392**)](https://www.reddit.com/r/vmware/comments/1g5k7ev/how_to_disable_hyperv_in_os_windows_11_home/)

**Step 1:** Create a text document and rename it as "Hyper-V.txt"

**Step 2:** Enter the following code into the document:

```cmd
pushd "%~dp0"
dir /b %SystemRoot%\servicing\Packages\*Hyper-V*.mum >hyper-v.txt
for /f %%i in ('findstr /i . hyper-v.txt 2^>nul') do dism /online /norestart /add-package:"%SystemRoot%\servicing\Packages\%%i"
del hyper-v.txt
Dism /online /enable-feature /featurename:Microsoft-Hyper-V-All /LimitAccess /ALL
```

**Step 3:** After saving the document, rename the .txt to .cmd, so the file should be "Hyper-V.cmd" now

**Step 4:** Right-click the document and execute the file as administrator. A command window will appear. After the installation is complete, enter Y to restart the computer

You should now have the Hyper-V option in "Turn Windows features on or off" menu.

### If you don't have : gpedit.msc on Windows 11 ?

[Source](https://www.malekal.com/comment-activer-gpedit-msc-windows-11/)

**Step 1:** Create a text document and rename it as "active-gpedit.txt"

**Step 2:** Enter the following code into the document:

```cmd
pushd "%~dp0"
dir /b %SystemRoot%\servicing\Packages\*Hyper-V*.mum >hyper-v.txt
for /f %%i in ('findstr /i . hyper-v.txt 2^>nul') do dism /online /norestart /add-package:"%SystemRoot%\servicing\Packages\%%i"
del hyper-v.txt
Dism /online /enable-feature /featurename:Microsoft-Hyper-V-All /LimitAccess /ALL
```

**Step 3:** After saving the document, rename the .txt to .cmd, so the file should be "active-gpedit.cmd" now

**Step 4:** Right-click the document and execute the file as administrator. A command window will appear. After the installation is complete, enter Y to restart the computer

```powershell
@echo off
pushd "%~dp0"

dir /b %SystemRoot%\servicing\Packages\Microsoft-Windows-GroupPolicy-ClientExtensions-Package~3*.mum >List.txt
dir /b %SystemRoot%\servicing\Packages\Microsoft-Windows-GroupPolicy-ClientTools-Package~3*.mum >>List.txt

for /f %%i in ('findstr /i . List.txt 2^>nul') do dism /online /norestart /add-package:"%SystemRoot%\servicing\Packages\%%i"
pause
```

You should now have the **Local Group Policy Editor** on our Windows 11.

---

## Some scripts :

- `hyper-v-install.cmd` :

```cmd
bcdedit /set hypervisorlaunchtype auto
DISM /Online /Enable-Feature /All /FeatureName:Microsoft-Hyper-V
DISM /Online /Enable-Feature /All /FeatureName:VirtualMachinePlatform
DISM /Online /Enable-Feature /All /FeatureName:Microsoft-Windows-Subsystem-Linux
shutdown /r /t 5
```

- `hyper-v-uninstall.cmd` :

```cmd
bcdedit /set hypervisorlaunchtype off
DISM /Online /Disable-Feature /FeatureName:Microsoft-Hyper-V-All
DISM /Online /Disable-Feature /FeatureName:VirtualMachinePlatform
DISM /Online /Disable-Feature /FeatureName:Microsoft-Windows-Subsystem-Linux
shutdown /r /t 5
```

---