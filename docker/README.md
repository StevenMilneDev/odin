# Docker
Connect: `ssh docker@192.168.1.140`

## Hosts
The Docker swarm is made up of the following VMs;

- docker-master (IP: `192.168.1.140`) The swarm master
- docker-01 (IP: `192.168.1.151`) A worker node
- docker-02 (IP: `192.168.1.227`) A worker node

## Services
The swarm hosts the following services;

- [Portainer](http://192.168.1.140:9000/) A web UI for managing the swarm
- [Nexus](http://192.168.1.140:8081/) A package repository for NPM, Docker, Ruby and more...
