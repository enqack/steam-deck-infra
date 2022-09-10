# Steam Deck Infrastructure

This project is used to manage software installs and manage backups of user data.

## Getting Started

### Steam Deck Preparation

Insert a blank SD card into you Steam Deck. Then enter desktop mode and open Konsole.

A password must be added to the user account. Enter the following into Konsole and you will be prompted to supply a password and confirm it ( characters will not be displayed as you enter the password ):

```
passwd
```

We must ensure your SD card is unmounted in order to partition and format it. In Konsole, enter the following:

```
sudo umount /dev/sda
sudo parted /dev/sda rm 1
sudo parted --script --align optimal -- /dev/sda mkpart primary 1MiB -2048s
mkfs.ext4 -L sdinfra /dev/sda1
```

Now re-insert the SD card. Then set permissions for the SD card. In Konsole, enter the following:

```
sudo chown $USER:$USER /run/media/$USER/sdinfra
```

Now clone the repository and set up Ansible. In Konsole, enter the following:

```
cd /run/media/$USER/sdinfra
git clone https://github.com/enqack/steam-deck-intra.git
cd steam-deck-intra
python3 -m venv .venv
source .venv/bin/activate
pip3 install -r python-req.txt
ansible-galaxy install -r ansible-req.yml
```

### Operations

Now you can run Ansible to install and configure the software. 

```
ansible-playbook playbooks/main.yml --ask-become-pass
```

Back-up your Steam Deck user files with the following command:

```
ansible-playbook playbooks/deck-backup.yml
```

Restore your Steam Deck user files with the following commands:

```
ansible-playbook playbooks/deck-restore.yml
```

### Additional Runs

Once Konsole is closed some configuration is lost. To re-run the above operations enter the following in a new Konsole window:

```
cd /run/media/$USER/sdinfra/steam-deck-infra
source .venv/bin/activate
```

## Overview

### Installed Software

* alacritty

* Flatseal
* Proton Up QT
* Bottles

* Steam ROM Manager
* DOSBox
* DuckStation
* xemu

* Discord
* OBS Studio
* VLC
* VS Code
* Spotify
* Krita
* Chrome
