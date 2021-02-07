# Kubernetes
The server contains a couple of Kubernetes clusters, managed by Rancher.

## Hosts
The Kubernetes clusters are serviced by a few VMs;

- kube-rancher (IP: `192.168.1.182`) A small Kubernetes cluster which allows management of other clusters.
- kube-master (IP: `192.168.1.98`) The control plane of the primary Kubernetes cluster
- kube-01 (IP: `000.000.000.000`) A worker node for the primary cluster
- kube-02 (IP: `000.000.000.000`) A worker node for the primary cluster

## Services
The cluster provides the following services;

- [Rancher](https://192.168.1.182/) A web UI for managing Kubernetes clusters
