# Steam Deck Infrastructure

This project is used to manage software installs and manage backups of user data.

## Getting Started

### Steam Deck Preparation

Enter desktop mode and open Konsole.

A password must be added to the user account. Enter the following into Konsole and you will be prompted to supply a password and confirm it ( characters will not be displayed as you enter the password ):

```
passwd
```

Next, generate a private key pair for Ansible to work correctly. Run the command below and follow the prompts.

```
ssh-keygen
```

Then copy the public key to your authorized keys. Run the command below and follow the prompts.

```
ssh-copy-id
```

Insert a blank SD card into your Steam Deck.

In Konsole, enter the following to format and mount your SD card.

```
sudo mkfs.ext4 -L sdinfra /dev/mmcblk0p1
udisksctl mount -b /dev/mmcblk0p1
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
ansible-playbook playbooks/deck-backup.yml --extra-vars "storage_path=/run/media/$USER/sdinfra"
```

Restore your Steam Deck user files with the following commands:

```
ansible-playbook playbooks/deck-restore.yml --extra-vars "storage_path=/run/media/$USER/sdinfra"
```

### Additional Runs

Once Konsole is closed some configuration is lost. To re-run the above operations enter the following in a new Konsole window:

```
cd /run/media/$USER/sdinfra/steam-deck-infra
source .venv/bin/activate
```

#### Warning

Once the Steam Deck is rebooted or the SD card is re-inserted it's mounting path with change to the following:

```
/run/media/sdinfra
```

## Overview

### Installed Software

* alacritty

* Flatseal
* Proton Up QT
* Bottles
* SDGBoop

* Steam ROM Manager
* DOSBox
* DuckStation
* xemu

* Bitwarden
* Discord
* OBS Studio
* VLC
* VS Code
* Spotify
* Krita
* Chrome
