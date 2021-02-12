# Kubernetes
The server contains a couple of Kubernetes clusters, managed by Rancher.

## Hosts
The Kubernetes clusters are serviced by a few VMs;

- kube-rancher (IP: `192.168.1.206`) A small Kubernetes cluster which allows management of other clusters.
- kube-master (IP: `192.168.1.184`) The control plane of the primary Kubernetes cluster
- kube-01 (IP: `192.168.1.236`) A worker node for the primary cluster
- kube-02 (IP: `192.168.1.97`) A worker node for the primary cluster

To add a new host to the cluster, install [k3os](https://k3os.io/); a dedicated Kubernetes operating system. Install k3os by booting from the iso and typing the command;

```
wget https://raw.githubusercontent.com/StevenMilneDev/odin/master/kubernetes/cloud-config.yml
sudo k3os install
```

## Services
The cluster provides the following services;

- [Rancher](https://192.168.1.182/) A web UI for managing Kubernetes clusters
