# How can you get systemd on your machine?

To get started, you will need to do these two things: – Ensure you are running the right version of WSL: Version 0.67.6 and above – Set the systemd flag set in your WSL distro settings
### Ensuring you are on the right WSL version

This change is only available in the Microsoft Store version of WSL version 0.67.6 and higher. You can check your version number by running `wsl --version`. If that command fails then you are running the in-Windows version of WSL and need to upgrade to the Store version.

This version of WSL is now available in the Microsoft Store to users on Windows Insiders build for initial testing, and then after a few weeks we will make it available to all users to ensure quality. You can run `wsl --update` to check for any WSL updates.

If you are not on Windows Insiders and want to use it immediately, you can download the latest release from the WSL release page.
### Set the systemd flag set in your WSL distro settings

You will need to edit the `wsl.conf` file to ensure systemd starts up on boot.

Add these lines to the `/etc/wsl.conf` (note you will need to run your editor with sudo privileges, e.g: sudo nano `/etc/wsl.conf`):

```
[boot]
systemd=true
```

And close out of the nano editor using `CTRL+O` to save and `CTRL+X` to exit.
### Final steps

With the above steps done, close your WSL distro Windows and `run wsl.exe --shutdown` from PowerShell to restart your WSL instances. Upon launch you should have systemd running. You can check this with the command `systemctl list-unit-files --type=service` which should show your services’ status.
