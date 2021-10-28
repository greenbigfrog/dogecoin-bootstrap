# Set up node on a VPS

### Requirements:
* Basic understanding of the linux ecosystem
* Connect to the VPS via ssh

## VPS requirements:
* minimum 2 Core's
* at least 4 GB RAM
* at least 50 GB disk space
* a lot of bandwidth (don't start unless you have at least 2 TB bandwidth)
One can get away with less, but I can't really recommend any less, although it will still work. (Well, diskspace requirement is always the same.)

## What VPS do I recommend:
I recommend using the `4 GB / 2 Cores CPU / 80 GB Storage` VPS from vultr. Feel free to use my affiliate link: https://www.vultr.com/?ref=7274718
Using the affiliate link https://www.vultr.com/?ref=8874276-6G will give you 100 USD to use within 30 days after signing up.

Alternatively you can also rent from vultr by using the reseller [bithost.io](https://bithost.io), paying with cryptocurrency via coinpayments.net.

Instructions are written to work with debian 10 as written below.

# How to set up a Dogecoin Core Full Node
1. Make sure your system is up to date:
```
apt update && apt upgrade
```
2. Get the binary files: 
```
wget https://github.com/dogecoin/dogecoin/releases/download/v1.14.4/dogecoin-1.14.4-x86_64-linux-gnu.tar.gz
```
3. Unpack the `tar.gz`: 
```
tar -zxvf dogecoin-1.14.4-x86_64-linux-gnu.tar.gz
```
4. Download the torrent file:
```
wget https://dogecoin.gg/files/dogecoin-bootstrap-2021-05-09.torrent
```
5. Install aria2:
```
apt install aria2
```
6. Download/Torrent the bootstrap: 
```
aria2c --bt-max-peers=0 dogecoin-bootstrap-2021-05-09.torrent
```
(For seeding (highly recommended): `aria2c --check-integrity=true --bt-max-peers=0 --seed-ratio=0 dogecoin-bootstrap-2021-05-09.torrent`)

7. Link the folders ("Hack" due to aria2c automatically creating a subfolder for  multi file torrent)
```
ln -s dogecoin-bootstrap-2021-05-09 .dogecoin
```
8. Set a `rpcuser` and `rpcpassword` in `~/.dogecoin/dogecoin.conf`:
```
echo "rpcuser=jdgjg
rpcpassword=dgskgdsk
disablewallet=1
maxconnections=64" >> ~/.dogecoin/dogecoin.conf
```
The default for `maxconnections` is 128, most machines struggle to keep up with this many connections. I've found ~64 to work on most machines if you follow my recommended specs.
9. Start up dogecoind:
```
~/dogecoin-1.14.4/bin/dogecoind &
```
10. You can check the status of your core wallet using:
```
~/dogecoin-1.14.4/bin/dogecoin-cli getinfo
```
11. If the `connections` in `getinfo` is greater then 8, you are successfully running a full core node!

### Tips (most tips are integrated into the install script)
* To prevent dogecoind from stopping as soon as you close the ssh connection: `apt install tmux` [TL;DR](https://github.com/tldr-pages/tldr/blob/master/pages/common/tmux.md)
* To make your VPS more secure, set up a firewall: `apt install ufw` (eg. `ufw allow 22`, `ufw allow 22556`, `ufw enable`
* Enable a swap file if your VPS has < 4GB Ram:
```
fallocate -l 4G /swapfile
chmod 600 /swapfile
mkswap /swapfile
swapon /swapfile
cp /etc/fstab /etc/fstab.bak
echo '/swapfile none swap sw 0 0' >> /etc/fstab
```

# Setting up multiple nodes
I recommend setting up one VPS, and then creating a bootstrap/backup, from which you then can create even more VPSs which don't have to sync with the blockchain anymore.

# Additional Settings you can add to your dogecoin.conf
```
maxuploadtarget=<MiB per day>
maxconnections=<num>
```


### Addnodes
```
~/dogecoin-1.14.2/bin/dogecoin-cli addnode dnf-1.gbf.re add
~/dogecoin-1.14.2/bin/dogecoin-cli addnode dnf-2.gbf.re add
~/dogecoin-1.14.2/bin/dogecoin-cli addnode dnf-3.gbf.re add
~/dogecoin-1.14.2/bin/dogecoin-cli addnode dnf-4.gbf.re add
~/dogecoin-1.14.2/bin/dogecoin-cli addnode doge1-eu.langerhans.de add
~/dogecoin-1.14.2/bin/dogecoin-cli addnode doge2-eu.langerhans.de add
~/dogecoin-1.14.2/bin/dogecoin-cli addnode doge3-eu.langerhans.de add
~/dogecoin-1.14.2/bin/dogecoin-cli addnode doge4-eu.langerhans.de add
```
