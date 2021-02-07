# HP Server
This repository contains information about the HP ProLiant DL380 G6 server.

## IP Addresses
There are various virtual machines running on the server. You can log into them at the following IP addrresses via SSH.

- docker `192.168.1.140` (username: `rancher`)
  - portainer `192.168.1.140:9000`
  - nexus `192.168.1.140:8081`
- docker-01 `192.168.1.151` (username: `rancher`)
- docker-02 `192.168.1.227` (username: `rancher`)
- kubernetes
  - kube-rancher https://192.168.1.182/
  - kube-master `ssh rancher@192.168.1.98`

## Links
- Portainer: http://192.168.1.140:9000
- Rancher: https://192.168.1.182/