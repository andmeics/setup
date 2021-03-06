## 1. Install the required packages

```
apt-get install unattended-upgrades apt-listchanges
```
## 2. Edit the configuration file
Put the lines below into the configuration file /etc/apt/apt.conf.d/50unattended-upgrades, everything that was originally inside the generated file can be removed before you add the lines below.

```
Unattended-Upgrade::Origins-Pattern {
    "origin=Debian,codename=${distro_codename},label=Debian-Security";
    "origin=TorProject";
};
Unattended-Upgrade::Package-Blacklist {
};
```
## 3. Automatically reboot
If you want to automatically reboot add the following at the the end of the file 

```
/etc/apt/apt.conf.d/50unattended-upgrades:
```

Unattended-Upgrade::Automatic-Reboot "true";
Update the file /etc/apt/apt.conf.d/20auto-upgrades with the following content

```
APT::Periodic::Update-Package-Lists "1";
APT::Periodic::AutocleanInterval "5";
APT::Periodic::Unattended-Upgrade "1";
APT::Periodic::Verbose "1";
```
## 4. Test
You can test your unattended-upgrades setup with the following command:

```
sudo unattended-upgrade -d
```
