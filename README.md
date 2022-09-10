# Steam Deck Infrastructure

This project is used to manage software installs and manage backups of user data.

## Getting Started

### Steam Deck Preparation

We must know where your SD card is mounted to create some directories.

Enter desktop mode and open Konsole, enter the following:

```
ls -l /run/media/deck/
# make note of your SD Card's name and use it on the next line
export sdcard=/run/media/deck/<sdcard>
mkdir ${sdcard}/rsync-backups
```

In order to proceed a password must be added to the user account. Enter the following and you will be prompted to supply a password and confirm it ( characters will not be displayed as you enter the password ).

```
passwd
```

Now clone the repository and set up Ansible. In the same Konsole window as before, enter the following:

```
cd $sdcard
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
ls $sdcard/rsync-backups | sort
# make note of backup timestamp to use for the operation
export timestamp=<2022-12-31-23-59-59>
ansible-playbook playbooks/deck-restore.yml
```

### Additional Runs

Once Konsole is closed some configuration is lost. To re-run the above operations enter the following in a new Konsole window:

```
ls -l /run/media/deck/
# make note of your SD Card's name and use it on the next line
export sdcard=/run/media/deck/<sdcard>
cd ${sdcard}/steam-deck-intra
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
