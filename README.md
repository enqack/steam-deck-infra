# Steam Deck Infrastructure

This project is used to manage flatpak software installs and manage back-ups of user data.

## Getting Started

### Steam Deck Preperation

We must know where your SD card is mounted to create some directories.

Enter desktop mode and open Konsole, enter the following:

```
ls -l /run/media/deck/
# make note of your SD Card's name and use it on the next line
export sdcard=/run/media/deck/<sdcard>
mkdir ${sdcard}/rsync-backups
```

Now clone the repository and set up Ansible.

In the same Konsole window as before, enter the following:

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
ansible-playbook main-playbook.yml
```

Back-up your Steam Deck user files with the following command:

```
ansible-playbook deck-backup.yml
```

Restore your Steam Deck user files with the following command:

```
ansible-playbook deck-restore.yml
```

### Additional Runs

Once Konsole is closed some configuration is lost. To re-run the above operations enter following in a new Konsole window:

```
ls -l /run/media/deck/
# make note of your SD Card's name and use it on the next line
export sdcard=/run/media/deck/<sdcard>
cd ${sdcard}/steam-deck-intra
source .venv/bin/activate
```

## Overview

### Installed Software

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
