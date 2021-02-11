# Docker
Connect: `ssh docker@192.168.1.140`

## Hosts
The Docker swarm is made up of the following VMs;

- docker-master (IP: `192.168.1.122`) The swarm master
- docker-01 (IP: `192.168.1.157`) A worker node
- docker-02 (IP: `192.168.1.182`) A worker node

### Adding a Host
To add a new host to the swarm, you must first provision a VM and attach the RancherOS installation ISO. Once the VM has started up, type this command to install RancherOS;

```
wget https://raw.githubusercontent.com/StevenMilneDev/odiin/master/docker/nodes/<NODE>/cloud-config.yml
sudo ros install -d /dev/sda /c cloud-config.yml
```

Once installed, eject the iso and reboot. The `cloud-config.yml` file contains the certifcate required to connect to the VM via SSH. Now connect to the machine using the command `ssh rancher@<IP>` where `<IP>` is the IP address of the machine. Once logged in, type the following command to connect it to the swarm;

```
docker swarm join --token SWMTKN-1-5gnkysij2l0qioc08ei75kgo2xew38vq6o9y5zv0erva3ilis4-0n2l379ec4lzn3ncje8dd1sgp 192.168.1.122:2377
```

## Services
The swarm hosts the following services;

- [Portainer](http://192.168.1.140:9000/) A web UI for managing the swarm
- [Nexus](http://192.168.1.140:8081/) A package repository for NPM, Docker, Ruby and more...
