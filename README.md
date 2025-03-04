# Ansible with Kubernetes

This repository demonstrates how to use Ansible to manage and configure Kubernetes pods. The setup involves creating a Kubernetes cluster, scaling a deployment, updating the container image, and then using Ansible to apply custom configurations to the running pods.

## Overview

1. **Kubernetes Cluster Setup**: 
   - A Kubernetes cluster was set up, and an `nginx` deployment was scaled to 3 replicas using the command:
     ```bash
     kubectl scale deployment nginx --replicas=3
     ```
   - The container image for the `nginx` deployment was updated to `tiangolo/uwsgi-nginx-flask:python3.9` using the command:
     ```bash
     kubectl set image deployment/nginx nginx=tiangolo/uwsgi-nginx-flask:python3.9
     ```

2. **Inventory Configuration**:
   - The names of the running pods were saved in an `inventory.yml` file. This file defines the connection details for each pod, including the namespace and pod name, using the `community.kubernetes.kubectl` connection plugin.

3. **Ansible Playbook**:
   - An Ansible playbook (`nginx_config.yml`) was created to configure the Nginx servers running in the Kubernetes pods. The playbook performs the following tasks:
     - Copies a custom Nginx configuration file to each pod.
     - Reloads the Nginx service to apply the new configuration.

4. **Execution**:
   - The playbook was executed using the command:
     ```bash
     ansible-playbook -i inventory.yml nginx_config.yml
     ```
   - This command applies the custom Nginx configuration to all pods defined in the `inventory.yml` file.

## Usage

To use this setup, follow these steps:

1. Ensure you have a running Kubernetes cluster and the `kubectl` command is configured to interact with it.
2. Scale your deployment and update the container image as needed.
3. Update the `inventory.yml` file with the names of your running pods.
4. Modify the `nginx_config.yml` playbook to suit your configuration needs.
5. Run the Ansible playbook to apply the configurations to your Kubernetes pods.

## Requirements

- Kubernetes cluster
- `kubectl` command-line tool
- Ansible installed on your local machine
- `community.kubernetes.kubectl` Ansible collection installed

## Notes

- Ensure that the `community.kubernetes.kubectl` collection is installed before running the playbook. You can install it using:
  ```bash
  ansible-galaxy collection install community.kubernetes
