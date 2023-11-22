## Generally useful Win10 (and 11) things

### Disable prompt on opening an executable:
1. Control panel > Internet options > Security > Custom level
2. Set ”Launching applications and unsafe files” to ”enable”

### Remove ”Share” from context menu:
1. Computer/HKEY_CLASSES_ROOT/*/shellex/ContextMenuHandlers/ModernSharing
2. Delete key ”ModernSharing”

Source: https://www.majorgeeks.com/content/page/remove_the_share_context_menu_in_windows_10.html

### Remove ”Give access to” from context menu:
1. HKEY_LOCAL_MACHINE/SOFTWARE/Microsoft/Windows/CurrentVersion/Shell Extensions
2. Create key ”Blocked” if it doesn't exist
3. Add empty string value named ”{f81e9010-6ea4-11ce-a7ff-00aa003ca9f6}”

Source: https://www.majorgeeks.com/content/page/remove_the_give_access_to_context_menu_in_windows_10.html

### Remove ”Send to” from context menu:
1. HKEY_CLASSES_ROOT/AllFilesystemObjects/shellex/ContextMenuHandlers/Send To
2. Open (Default) and clear its value

Source: https://www.isumsoft.com/windows-10/remove-or-restore-the-send-to-context-menu.html

### Remove ”Restore previous versions” from context menu:
1. HKEY_LOCAL_MACHINE/SOFTWARE/Microsoft/Windows/CurrentVersion/Shell Extensions
2. Create key ”Blocked” if it doesn't exist
3. Add empty string value named ”{596AB062-B4D2-4215-9F74-E9109B0A8153}”

Source: https://www.thewindowsclub.com/remove-restore-previous-versions-context-menu

### Remove ”Include in library” from context menu:
1. HKEY_CLASSES_ROOT/Folder/ShellEx/ContextMenuHandlers
2. Delete key ”Library Location”

Source: https://winaero.com/remove-include-library-windows-10/

### Remove ”Cast to device” from context menu:
1. HKEY_LOCAL_MACHINE/SOFTWARE/Microsoft/Windows/CurrentVersion/Shell Extensions
2. Create key ”Blocked” if it doesn't exist
3. Add empty string value named ”{7AD84985-87B4-4a16-BE58-8B72A5B390F7}”

Source: https://www.howtogeek.com/720449/how-to-remove-cast-to-device-option-from-windows-10-context-menu/

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
```
