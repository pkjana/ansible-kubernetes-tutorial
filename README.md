# ansible-kubernetes-tutorial
kubernetes operation by ansible host

# Deploying applications to Kubernetes using Ansible

## Prerequisite 
1. Ansible controller host 
2. Kubernetes cluster ( one control plane node and two worker node)



## 1. Set up Ansible Control node

On your Ansible Control node, run the following to install Kubernetes Collection (this includes the module and plugins)

$ sudo ansible-galaxy collection install kubernetes.core

$ sudo ansible-galaxy collection install community.kubernetes

$ sudo ansible-galaxy collection install cloud.common


$ sudo apt update

$ sudo apt install python3-pip

Install python3-kubernetes package in control plane node
$ sudo pip install kubernetes or $ sudo apt install python3-kubernetes

