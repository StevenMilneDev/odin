# Node Setup - kube-rancher
The kube-rancher node hosts a separate cluster just for Rancher. To set the node up you must first follow the standard instructions for a Docker host and install RancherOS.

```
wget https://raw.githubusercontent.com/StevenMilneDev/odin/master/kubernetes/nodes/<NODE>/cloud-config.yml
sudo ros install -d /dev/sda -c cloud-config.yml
```

Once RancherOS is installed you can SSH into the machine and type the following command;

```
docker run -d --restart=unless-stopped -p 80:80 -p 443:443 -v /opt/rancher:/var/lib/rancher --privileged --name rancher rancher/rancher:latest
```