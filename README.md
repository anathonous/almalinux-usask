<p align="center"><img src=logo.png width="600"></p><br>

How to properly configure Alma Linux Immutable Atomic for USask Environment


 - Lang
 - Time Server
 - Partitioning
 - Encryption

# Alma Linux Atomic installation 

## Pre-installation setup

Download latest version of AlmaLinux Atomic.<br>
https://github.com/AlmaLinux/atomic-desktop<br>
Download latest ISO of Alma Linux Immutable. Highly recommend KDE.<br><br>

Download Fedora Media Writer<br>
https://github.com/FedoraQt/MediaWriter<br>

Write to USB Key. Atleast 6GB. <br>

## Lang
Set to CA English
## Keyboard
Set to US English
## Networking
Connect to USask. WPA3 PEAP<br>
Domain usask.ca<br>
Username abc123@usask.ca<br>
Password pawspassword<br>
## Time
Set timezone<br>
Set ntpserver to time.nrc.ca
## User
Create Basic Username Password

## Partitions
### Creating partitions

 - Choose Install Destination
 - Choose Custom
 - Choose disk. Click Done
 - Based on the assumption you do not intend on dual booting
 - Choose "New mount points will use"
 - Change to Btrfs
 - Enable Encrypt Data
 - Then click "Click here to create them Automatically."
 - Choose Blue "Done" at top left hand corner
 - Enter passphrase for encryption twice. Save.
 - Click continue. This will repartition drive. (you will lose everything on the drive. Maybe use windows media creator to create a spare windows installer usb)
 - Begin install.

### Setup Discover
Open Discover, Go to settings, Click on "Add Flathub".

### Install Podman Desktop
Install Podman Desktop from Discover

### Install Virt-Manager

Open Terminal.

    sudo rpm-ostree install virt-manager qemu-kvm qemu libvirt
    sudo rpm-ostree kargs --append="intel_iommu=on" --append="iommu=pt" (for INTEL)
    sudo rpm-ostree kargs --append="amd_iommu=on" --append="iommu=pt"  (for AMD)
    sudo systemctl reboot
    sudo systemctl enable --now libvirtd
    sudo systemctl enable --now virtnetworkd.service
    

### Enable Firewall

Open Firewall settings and change default zone to block.

### Install Browser

Install Waterfox via Discover. Install Flatpak

### Install other software
````
sudo rpm-ostree install kmail
````

### In closing
You now have a Btrfs subvolumed system that is immutable. You can create system snapshots for backups using snapper. As well as export Atomic Deployments.<br>
If you do your software development in Podman(docker) your software is now reproducible on any other systems using podman/docker. Use 10-minimal for your docker images. <br>
You now have the ability to create virtual machines and keep other software contained within a VM.<br>
All of your Flatpak software is also containerized. Your baseOS should be rock solid.<br>
To update.<br>
Just<br>
    sudo rpm-ostree update
<br><br>
This makes everything you do extremely containerize and reproducible.
