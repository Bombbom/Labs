# Network labs 

## Manual Installation

- Install any Linux distribution
- Install docker (https://docs.docker.com/engine/install/)
- Install lldpd : apt install lldpd 
- Allow USER to use docker, adding to docker group: sudo usermod -aG docker user_name
- Add to scripts on the scripts directory to user home directory: 
    - git clone https://github.com/brnuts/netlab.git
    - cp scripts/* /home/netlab
- Install python3 and pip
- configure update-hosts.service by copying update-hosts scripts to /etc/systemd/system: cp update-hosts.* /etc/systemd/system/
- enable update-hosts: systemctl enable update-hosts.service
- start update-hosts: systemctl start update-hosts
- run scrip to start all containers: ./start-containers.sh

## Checks 