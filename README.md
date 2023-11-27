# Polkit-helper
A small script creating PolKit rules, allowing wheel users to execute tasks like mounting LUKS drives, starting virt-manager and anything you like.

## Use case:

On fedora (and probably other Distros) many apps are permitted to run without a sudo password prompt. This is quite annoying, especially when automounting LUKS drives or wanting to use virt-manager.

Infos:

- [Wikipedia](https://en.wikipedia.org/wiki/Polkit)
- [RedHat (with example)](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/7/html/desktop_migration_and_administration_guide/policykit)
- [Debian Wiki, explaining the difference to Policykit](https://wiki.debian.org/PolicyKit)
- [Arch wiki with more infos on Desktop implementations](https://wiki.archlinux.org/title/Polkit)

Install:

```
wget https://github.com/trytomakeyouprivate/Polkit-helper/raw/main/create-polkit-rule -P ~/.local/bin/ && chmod +x ~/.local/bin/create-polkit-rule && echo "Polkit rule helper installed."
```

## How to use

- Try to execute an app and see the password prompt, on KDE click on "show details" and copy the process ID
- Launch the script in the Terminal by entering `create-polkit-rule`
- Enter any name (without empty spaces) to name the rule.
- Paste the processes name 

Be careful not to allow critical processes to run without a password prompt!

## Examples:

Unlocking and mounting LUKS drives:

- org.freedesktop.udisks2.encrypted-unlock-system
- org.freedesktop.udisks2.filesystem-mount-system

Using virt-manager:

- ~~org.libvirt.unix.manage~~

This is done by adding the user to the group `libvirt` !

```
sudo groupadd libvirt
sudo usermod -aG libvirt $USER
```
