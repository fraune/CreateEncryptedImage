# CreateEncryptedImage

## Description

This macOS workflow (`Create Encrypted Image.workflow`) is an Automator Quick Action, which adds a context popup on folders in Finder. When activated, the workflow launches a new Terminal window that helps users encrypt a folder and its contents. The resulting DMG disk image requires a password to unlock.

## How to install it

1. Download this repository as a .zip file
<img width="420" alt="Download fepository as ZIP" src="https://github.com/fraune/CreateEncryptedImage/assets/52302810/39f912e0-347e-4a53-90d1-8a727393c3ba">
2. Right click `Create Encrypted Image.workflow`, and select Open With Automator Installer
<img width="886" alt="Install the workflow" src="https://github.com/fraune/CreateEncryptedImage/assets/52302810/67652e7d-90b0-46a0-9a06-129a504095d9">
3. Click Install to register the quick action
<img width="503" alt="Register the quick action" src="https://github.com/fraune/CreateEncryptedImage/assets/52302810/5c6b2eae-10c0-45ee-93e2-467198bc4309">
4. Confirm installation, by right clicking a folder, and checking that Quick Actions now contains the workflow
<img width="538" alt="Confirm quick action enabled" src="https://github.com/fraune/CreateEncryptedImage/assets/52302810/27572c24-e352-4e08-b468-d0e1686d83d9">
5. A Terminal window will prompt for `sudo`, which is your Mac admin's password. It is required to run the command.
6. You will be prompted for a password to encrypt the folder with. This is distinct from the `sudo` password, and will be required to decrypt the DMG.
<img width="711" alt="Encrypting a folder" src="https://github.com/fraune/CreateEncryptedImage/assets/52302810/acc6622e-0f20-4dc2-8cd5-17fdc0a4f42f">
7. You should see a new file appear at the same location as the folder you encrypted. Double-click it, then enter your password to decrypt it.
<img width="600" alt="Decrypt the image" src="https://github.com/fraune/CreateEncryptedImage/assets/52302810/2de7843d-31b1-4796-a377-51556b590c48">

## Script contents

```applescript
on run {input, parameters}
    set folderPath to POSIX path of item 1 of input
    
    tell application "Terminal"
        activate
        do script "sudo hdiutil create -size 20mb -fs apfs -encryption AES-256 " & quoted form of folderPath & " -srcfolder " & quoted form of folderPath & "; exit"
    end tell
    
    return input
end run
```
