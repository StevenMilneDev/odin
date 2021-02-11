# Docker
Connect: `ssh docker@192.168.1.140`

## Hosts
The Docker swarm is made up of the following VMs;

- docker-master (IP: `192.168.1.140`) The swarm master
- docker-01 (IP: `192.168.1.151`) A worker node
- docker-02 (IP: `192.168.1.227`) A worker node

### Adding a Host
To add a new host to the swarm, you must first provision a VM and attach the RancherOS installation ISO. Once the VM has started up, type this command to install RancherOS;

```
wget https://raw.githubusercontent.com/StevenMilneDev/odiin/master/docker/nodes/<NODE>/cloud-config.yml
sudo ros install -d /dev/sda /c cloud-config.yml
```

## Services
The swarm hosts the following services;

- [Portainer](http://192.168.1.140:9000/) A web UI for managing the swarm
- [Nexus](http://192.168.1.140:8081/) A package repository for NPM, Docker, Ruby and more...
