# Ansible Role: nginx_k8s_role

This role manages the deployment and uninstallation of Nginx in a Kubernetes cluster.

## Requirements
- Ansible `kubernetes.core` collection installed
- Access to the Kubernetes cluster via kubeconfig

## Variables
- `k8s_namespace`: Kubernetes namespace (default: `default`)
- `nginx_deployment_name`: Name of the Nginx deployment (default: `nginx-deployment`)
- `nginx_service_name`: Name of the Nginx service (default: `nginx-service`)
- `nginx_image`: Nginx image to use (default: `nginx:latest`)
- `nginx_replicas`: Number of replicas (default: `1`)

## Usage

### Deploy Nginx
```yaml
- hosts: localhost
  roles:
    - role: nginx_k8s_role
      vars:
        action: deploy
```

### Uninstall Nginx
```yaml
- hosts: localhost
  roles:
    - role: nginx_k8s_role
      vars:
        action: uninstall


# 1. Set up Ansible Control node

On your Ansible Control node, run the following to install Kubernetes Collection (this includes the module and plugins)

$ sudo ansible-galaxy collection install kubernetes.core

$ sudo ansible-galaxy collection install community.kubernetes

$ sudo ansible-galaxy collection install cloud.common


$ sudo apt update

$ sudo apt install python3-pip

$ sudo pip install kubernetes
