## Generally potentially useful Win10 (and 11) things

Note that you should only use any of these if you know what you're doing and e.g. practice proper backuping practices and internet hygiene when it comes to stuff like downloaded files. Also this is not a list where each entry is equally useful; see which ones are helpful to you, if any, and apply them.

### Disable prompt on opening an executable or file Windows considers unsafe:
1. Control panel > Internet options > Security > Custom level
2. Set ”Launching applications and unsafe files” to ”enable”

### Disable Windows trying to report program crashes to Microsoft:
1. Run > services.msc
2. Stop service ”Windows Error Reporting Service” and set ”Startup type” to ”Disabled”

### Disable Win11 upgrade nagging:
- Go to https://aka.ms/WindowsTargetVersioninfo and make note of the latest version number for Windows 10, at time of writing that's 22H2
- Via group policies (Win10 Pro only):
  1. Run > gpedit.msc
  2. Computer Configuration > Administrative Templates > Windows Components > Windows Update > Windows Update for Business
  3. Select "Select target Feature Update version" and enable it
  4. Fill in the product and version fields with "Windows 10" and the version retrieved above
- Via registry:
  1. HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows\WindowsUpdate
  2. Set/add string with name "ProductVersion" and value "Windows 10"
  3. Set/add string with name "TargetReleaseVersionInfo" and the value being the version retrieved above
  4. Set/add dword with name "TargetReleaseVersion" and value 1

Source: https://cohost.org/Hempuli/post/3622800-decided-to-list-some#comment-aeae3d91-0317-42d8-824f-7814c52b4064

### Restore Win10 context menu in Win11:
- reg.exe add "HKCU\Software\Classes\CLSID\{86ca1aa0-34aa-4e8b-a509-50c905bae2a2}\InprocServer32" /f /ve
  - Restore new context menu: reg.exe delete "HKCU\Software\Classes\CLSID\{86ca1aa0-34aa-4e8b-a509-50c905bae2a2}" /f
 
### Disable XBox Game Bar:
1. HKEY_CURRENT_USER\SOFTWARE\Microsoft\Windows\CurrentVersion\GameDVR
2. Set/add dword named "AppCaptureEnabled" with value 0
3. HKEY_CURRENT_USER\System\GameConfigStore
4. Set/add dword named "GameDVR_Enabled" with value 0

Source: https://cohost.org/Hempuli/post/3622800-decided-to-list-some#comment-cc4ecbb5-f995-4b14-a225-4d87d538a067

### Disable Start Menu Bing searches:
1. HKEY_CURRENT_USER\Software\Policies\Microsoft\Windows\Explorer
2. Set/add dword named "DisableSearchBoxSuggestions" with value 1

### Remove ”Share” from context menu:
1. Computer\HKEY_CLASSES_ROOT\*\shellex\ContextMenuHandlers\ModernSharing
2. Delete key ”ModernSharing”

Source: https://www.majorgeeks.com/content/page/remove_the_share_context_menu_in_windows_10.html

### Remove ”Give access to” from context menu:
1. HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Shell Extensions
2. Create key ”Blocked” if it doesn't exist
3. Add empty string value named ”{f81e9010-6ea4-11ce-a7ff-00aa003ca9f6}”

Source: https://www.majorgeeks.com/content/page/remove_the_give_access_to_context_menu_in_windows_10.html

### Remove ”Send to” from context menu:
1. HKEY_CLASSES_ROOT\AllFilesystemObjects\shellex\ContextMenuHandlers\Send To
2. Open (Default) and clear its value

Source: https://www.isumsoft.com/windows-10/remove-or-restore-the-send-to-context-menu.html

### Remove ”Restore previous versions” from context menu:
1. HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Shell Extensions
2. Create key ”Blocked” if it doesn't exist
3. Add empty string value named ”{596AB062-B4D2-4215-9F74-E9109B0A8153}”

Source: https://www.thewindowsclub.com/remove-restore-previous-versions-context-menu

### Remove ”Include in library” from context menu:
1. HKEY_CLASSES_ROOT\Folder\ShellEx\ContextMenuHandlers
2. Delete key ”Library Location”

Source: https://winaero.com/remove-include-library-windows-10/

### Remove ”Cast to device” from context menu:
1. HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Shell Extensions
2. Create key ”Blocked” if it doesn't exist
3. Add empty string value named ”{7AD84985-87B4-4a16-BE58-8B72A5B390F7}”

Source: https://www.howtogeek.com/720449/how-to-remove-cast-to-device-option-from-windows-10-context-menu/

### Remove ”Print” from Win10 context menu:
- Add empty string value named ”ProgrammaticAccessOnly” to the following registry entries:
  - HKEY_CLASSES_ROOT\SystemFileAssociations\image\shell\print
  - HKEY_CLASSES_ROOT\batfile\shell\print
  - HKEY_CLASSES_ROOT\cmdfile\shell\print
  - HKEY_CLASSES_ROOT\docxfile\shell\print
  - HKEY_CLASSES_ROOT\fonfile\shell\print
  - HKEY_CLASSES_ROOT\htmlfile\shell\print
  - HKEY_CLASSES_ROOT\inffile\shell\print
  - HKEY_CLASSES_ROOT\inifile\shell\print
  - HKEY_CLASSES_ROOT\JSEFile\Shell\Print
  - HKEY_CLASSES_ROOT\otffile\shell\print
  - HKEY_CLASSES_ROOT\pfmfile\shell\print
  - HKEY_CLASSES_ROOT\regfile\shell\print
  - HKEY_CLASSES_ROOT\rtffile\shell\print
  - HKEY_CLASSES_ROOT\ttcfile\shell\print
  - HKEY_CLASSES_ROOT\ttffile\shell\print
  - HKEY_CLASSES_ROOT\txtfile\shell\print
  - HKEY_CLASSES_ROOT\VBEFile\Shell\Print
  - HKEY_CLASSES_ROOT\VBSFile\Shell\Print
  - HKEY_CLASSES_ROOT\WSFFile\Shell\Print
  - ...And a bunch of others too in the HKEY_CLASSES_ROOT -folder (e.g. OpenOffice filetypes)
 
Source: https://winaero.com/remove-print-context-menu-in-windows-10/

### Disable Windows updates (probably not a great idea):
- Method 1:
  1. Settings > Update & Security > Windows Update > Advanced options
  2. Disable ”Receive updates for other Microsoft products when you update Windows”
- Method 2:
  1. Run > services.msc
  2. Stop service ”Windows Update” and set ”Startup type” to ”Disabled”
- Method 3 (Win10 Pro only):
  1. Run > gpedit.msc
  2. Computer Configuration > Administrative Templates > Windows Components > Windows Update > Configure Automatic Updates
  3. Set to ”Disabled”

Source: https://answers.microsoft.com/en-us/windows/forum/all/system-keeps-nagging-me-with-win11-update/ffb4a450-6640-429a-9d8d-4dc2a4b6ce95

### Prevent AI Copilot in Win10 or Win11:
1. HKEY_CURRENT_USER\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\Advanced
2. Add dword named ”ShowCopilotButton” with value 0
3. HKEY_CURRENT_USER\SOFTWARE\Policies\Microsoft\Windows
4. Add key ”WindowsCopilot” if it doesn't exist
5. Add dword named ”TurnOffWindowsCopilot” with value 1

Source: https://cohost.org/purpleraccoon/post/3617693-if-you-re-stuck-on-w

### Delete/access file controlled by TrustedInstaller:
1. Right click > Properties > Security > Advanced
2. Click ”Change permissions” in bottom-left
3. Click ”Change” next to ”Owner:”
4. Enter ”Administrators” in the text field, click ”Check Names” to fill the rest & press Ok
5. Check the ”replace all child object permissions...” and press Ok
1. Some subfolders/-files might still not change, edit those separately in the same way
6. Back in Security, click Edit... and check all boxes for Administrators

### Restore old Windows Photo Viewer:
1. Create a .reg file with the code from "Restore_Windows_Photo_Viewer_ALL_USERS_with_Sort_order_fix.txt"
2. Run the .reg file

Code by Shawn Brink

Source: https://www.tenforums.com/tutorials/14312-restore-windows-photo-viewer-windows-10-a.html

### Generally useful utilities:
```
AutoRun
WinDirStat / WizTree
FileTypesMan
KeePassX
Process Explorer (Pexplorer/procexp)
ResourceHacker
TCPview
Powertoys:
  https://learn.microsoft.com/en-us/windows/powertoys
Upgraded command prompt:
  https://learn.microsoft.com/en-us/windows/terminal/install
Windows package manager:
  https://learn.microsoft.com/en-us/windows/package-manager/winget/
```

### Handy inbuilt tools:
```
Run > services.msc
Run > gpedit.msc
dxdiag.exe
regedit.exe
```
