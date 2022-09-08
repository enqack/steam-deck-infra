# Steam Deck Infrastructure

## Steam Deck Preperation

We must know where your SD card is mounted to create some directories.

Enter desktop mode and open Konsole, enter the following:

```
ls -l /run/media/deck/
# make note of your SD Card's name and use it on the next line
export sdcard=/run/media/deck/<sdcard>

rsyncdir=${sdcard}/rsync-backups
mkdir ${rsyncdir}
```

## Getting Started

In Konsole, enter the following:

```
cd $sdcard
git clone https://github.com/enqack/steam-deck-intra.git
cd steam-deck-intra
python3 -m venv .venv
source .venv/bin/activate
pip3 install -r python-req.txt
ansible-galaxy install -r ansible-req.yml
ansible-playbook main-playbook.yml
```

