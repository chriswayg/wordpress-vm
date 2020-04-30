# Wordpress VM
[![Build Status](https://travis-ci.org/chriswayg/wordpress-vm.svg?branch=master)](https://travis-ci.org/chriswayg/wordpress-vm)

### modified scripts for use on Proxmox KVM
Tested install on this VM template: Vanilla [Ubuntu 18.04 (bionic) Packer Template](https://github.com/chriswayg/packer-proxmox-templates/tree/master/ubuntu-18.04-amd64-proxmox)

### Documantation
- https://www.techandme.se
- https://www.hanssonit.se/wordpress-vm/

### Features
- Ubuntu 18.04
- MariaDB 10.2
- NGINX 1.16
- PHP-FPM 7.2
- Latest Wordpress (updates automatically)
- WP-CLI
- Redis Cache
- and [more](https://docs.hanssonit.se/s/W6fMouPiqQz3_Mog/virtual-machines-vm/d/W7jL1OPiqQz3_MtV/wordpress-vm-machine-configuration).

---
## Step-by-step wordpress-vm script

### Preparation

- Configure the VM in Proxmox with 2 GB RAM and 2 cores

- Login via SSH or serial console as default user (deploy) und become root
  `sudo su -`

- Download and run the wordpress-vm install script

  ```sh
  git clone https://github.com/chriswayg/wordpress-vm.git && cd wordpress-vm && chmod +x wordpress_install.sh

  ./wordpress_install.sh
  ```

### Prompt & response (example)

- create user: Y (is needed)
  `wordpress`

- find a better mirror? Y (N causes error)
- change keyboard layout? N

- *(after installation it will reboot)*

- login: `wordpress`
  - password:
  - [sudo] password for wordpress:


- change keyboard layout? N
- change timezone? Y
- find a better mirror? N
- configuration file sshd_config? keep the local version currently installed

- Which apps do you want to install?
  - [] Fail2ban
  - [*] Webmin
  - [*] Adminer


- Extra configurations
  - [] Security
  - [*] Static IP


- connected via SSH? N

- enter the static IP
  - `10.10.10.220/24`
  - correct? Y


- gateway address
  - 10.10.10.1`
  - correct? Y


- *(press ENTER within 120 s)*

- change the system user password

- Install Let's Encrypt certificate
  - install SSL (certificate)? Y
  - sure? Y
  - forwarded port 80+443? Y
  - have a domain? Y
  - enter the domain name you will use for Wordpress
    `www.example.org`
    - correct? Y
  - email address? `chris@gmail.com`


- Wordpress FQDN *(and main admin User)*
  - `https://www.example.org`
  - username:
    `chris`
  - password:
  - email:
    `chris@gmail.com`
  - correct? Y


- Upgrading - Congratulations *(and it will reboot again)*

#### Test it at

https://www.example.org/wp-login.php


#### Compare with VM-appliance supplied by hanssonit.se

```
# uncompress vmware archive, then use
qm importdisk 10100 Wordpress_VM_www.hanssonit.se-disk1.vmdk local -format qcow2
```
