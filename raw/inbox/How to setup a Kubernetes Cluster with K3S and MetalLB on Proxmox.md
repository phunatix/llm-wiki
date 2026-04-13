---
title: How to setup a Kubernetes Cluster with K3S and MetalLB on Proxmox
source: https://blog.chicho.com.ar/how-to-deploy-a-kubernetes-cluster-with-k3s/
author:
  - "[[Ruben Dario Coria]]"
published: 2024-02-14
created: 2026-02-12
description: "After to to learn K8s basic theory, its time to apply the knowledge on practice! Let's install K3s inside my little home lab with Proxmox.Requirements: * 3 VMs with Ubuntu 22.04 LTS * kubectlThe VMs were created from a template with Ubuntu 22.04 and cloud-initFor these example"
tags:
  - clippings
  - k3s
  - metallb
  - k8s
---
After to to learn K8s basic theory, its time to apply the knowledge on practice! Let's install K3s inside my little home lab with Proxmox.

Requirements:

- 3 VMs with Ubuntu 22.04 LTS
- kubectl

The VMs were created from a template with Ubuntu 22.04 and cloud-init

For these example I used 1 node master and 2 nodes workers

1. K3s-master - IP 192.168.52.229
2. k3s-worker1 - IP 192.168.52.228
3. k3s-worker2 - IP 192.168.52.227

We need to change the IP from dynamic to static.

```shell
##Example

# This file is generated from information provided by the datasource.  Changes
# to it will not persist across an instance reboot.  To disable cloud-init's
# network configuration capabilities, write a file
# /etc/cloud/cloud.cfg.d/99-disable-network-config.cfg with the following:
# network: {config: disabled}
network:
    version: 2
    renderer: networkd
    ethernets:
        eth0:
            addresses:
                - 192.168.52.228/24
            nameservers:
                addresses: [8.8.8.8, 8.8.4.4, 192.168.52.1]
            routes:
                - to: default
                  via: 192.168.52.1
```

Add the hostname of the VMS in the hosts file of each other.

```shell
echo -e "192.168.52.229 K3s-master" | sudo tee -a /etc/hosts
echo -e "192.168.52.228 K3s-worker1" | sudo tee -a /etc/hosts
echo -e "192.168.52.227 K3s-worker2" | sudo tee -a /etc/hosts
```

💡

In my particular case, was not necessary to change the hostname in each VM. But if you need to change it, you must use the next command:

```shell
#master node
sudo hostnamectl set-hostname K3s-master

#worker node
sudo hostnamectl set-hostname k3s-worker1
sudo hostnamectl set-hostname k3s-worker2
```

## Install K3s

### Master node

Inside the Master node, we need to disable the load balancer for default (kippler-db), because for this lab we're going to install MetaLB as a LoadBalancer.

Also we must disable Traefik for use Nginx Ingress Controller as ingress service instead of Traefik.

```shell
curl -sfL https://get.k3s.io | INSTALL_K3S_EXEC="server --disable traefik --disable servicelb" sh -
```

Once the K3s installation is completed in master node, we need to obtain the token for install the worker nodes.

```shell
sudo cat /var/lib/rancher/k3s/server/node-token
```

### Worker Node

With the token obtained from the "node-token" file, we must run the next command to add the worker nodes.

```shell
curl -sfL https://get.k3s.io | K3S_URL=https://ip_master_node:6443 K3S_TOKEN=<node-token> sh -
```

---

## Connect your cluster remotely

Copy the k3s.yaml file content

```shell
#path k3s file
/etc/rancher/k3s/k3s.yaml
```

Create a config file on your local machine and copy the k3s file content inside.

```shell
touch $HOME/.kube/config
```

Open your config file and change the address IP from 127.0.0.1 to <your\_server\_ip>:6443

```shell
apiVersion: v1
clusters:
- cluster:
    certificate-authority-data: <Secret>
    server: https://<your_server_ip>:6443
  name: default
```

Now you can use kubectl

```shell
$ kubectl get nodes
NAME          STATUS   ROLES                  AGE    VERSION
k3s-worker2   Ready    <none>                 178d   v1.27.4+k3s1
k3s-worker1   Ready    <none>                 178d   v1.27.4+k3s1
k3s-master    Ready    control-plane,master   178d   v1.27.4+k3s1
```

---

## Install MetalLB

When we work with K8s implementations on the cloud (AWS EKS, Azure EKS or Google GKE) we can create in native form a Service type "Load Balancer", but in baremetal cluster plataforms we need to deploy this kind of service.  
For this homelab we're going to deploy MetalLB as a LoadBalancer.

Requirements:

- A K8s Cluster
- Some IPV4 IP reserved for MetalLB
- Helm
- Kubectl
```shell
#1 - Add MetalLB respository to Helm
helm repo add metallb https://metallb.github.io/metallb

#2 - Update Helm repo
helm repo update

#3 - Create a MetalLB namespace
kubectl create namespace metallb

#4 - Install metalLB
helm install metallb metallb/metallb --namespace metallb

#5 - Confirm that the deploy was successful
kubectl -n metallb get pod
```

Configure the reserved an IP address pool with the Layer2 metod. I have a Mikrotik router where I reserve the ip range 192.168.52.30 - 192.168.52.80

```shell
# Metallb address pool
apiVersion: metallb.io/v1beta1
kind: IPAddressPool
metadata:
  name: cluster-pool
  namespace: metallb
spec:
  addresses:
  - 192.168.52.30-192.168.52.80

---
# L2 configuration
apiVersion: metallb.io/v1beta1
kind: L2Advertisement
metadata:
  name: metallb-homelab
  namespace: metallb
spec:
  ipAddressPools:
  - cluster-pool
```

---

## Load Balancer test

To test te correct operation of the load balancer we are going to deploy Nginx

```shell
#Create deploy
kubectl create deploy nginx --image=nginx

#Expose the deploy as a LoadBalancer type
kubectl expose deploy nginx --port=80 --target-port=80 --type=LoadBalancer

#Verify
kubectl get svc nginx
NAME    TYPE           CLUSTER-IP     EXTERNAL-IP     PORT(S)        AGE
nginx   LoadBalancer   10.43.60.115   192.168.52.30   80:32676/TCP   5h19m
```

Using the curl command we can see the successful response

```shell
$ curl 192.168.52.30:80
<!DOCTYPE html>
<html>
<head>
<title>Welcome to nginx!</title>
<style>
html { color-scheme: light dark; }
body { width: 35em; margin: 0 auto;
font-family: Tahoma, Verdana, Arial, sans-serif; }
</style>
</head>
<body>
<h1>Welcome to nginx!</h1>
<p>If you see this page, the nginx web server is successfully installed and
working. Further configuration is required.</p>

<p>For online documentation and support please refer to
<a href="http://nginx.org/">nginx.org</a>.<br/>
Commercial support is available at
<a href="http://nginx.com/">nginx.com</a>.</p>

<p><em>Thank you for using nginx.</em></p>
</body>
</html>
```

This was a minimal guide about how to deploy a baremetal K8s cluster, on the next post we're going to install Nginx Ingress Controller to expose the services outside our network.