What is Kubeadm
===============


The kubeadm tool is used to bootstrap smaller Kubernetes clusters so that we can experience all the kubernetes features. The cluster spin-up using kubeadm is eligible to pass the Kubernetes Conformance Program. The cluster life-cycle functions and cluster upgrades are also supported by kubeadm.

**Prerequisites**

1. One or more linux machines.
2. 2 GB 2 CPU machines if heavy apps running. 
3. 2GB 2 CPU server for master.
4. Full network connectivity between servers. 

Goals
=====

One master node
one worker node

Install dependecies on both servers. 
==========================================

Please verify the "depndency.sh". You can use the shell script in two ways. 

     wget https://github.com/liminpb/kubeadm-localstorage-cluster/blob/master/depndency.sh
     chmod 777 docker-kube-install.sh
     sh docker-kube-install.sh

Setting Up the Master Node
===========================

**Initialize the cluster**

**1. sudo kubeadm init --pod-network-cidr=10.244.0.0/16**

This command will give you a uniq Join command we need to apply in our worker nodes. So we have to copy and keep that safe after the master setup. 

**2.  Set up local kubeconfig**

 * "mkdir -p $HOME/.kube"

* "sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config"

* "sudo chown $(id -u):$(id -g) $HOME/.kube/config"

**3.  Apply Calco CNI**

     kubectl apply -f https://docs.projectcalico.org/v3.14/manifests/calico.yaml
     






