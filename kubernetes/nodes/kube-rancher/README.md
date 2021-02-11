# Node Setup - kube-rancher
The kube-rancher node hosts a separate cluster just for Rancher. To set the node up you must first follow the standard instructions for a Docker host and install RancherOS.

Once RancherOS is installed you can SSH into the machine and type the following command;

```
docker run -d --restart=unless-stopped -p 80:80 -p 443:443 --privileged --name rancher rancher/rancher:latest
```