# 🏠 Homelab

## 📕 Overview

This is a GitOps FluxCD based repository that manages my K3s Kubernetes cluster with each node virtualized through Proxmox. It was deployed using the following Ansible script: https://github.com/k3s-io/k3s-ansible

I'm currently building this homelab to learn Kubernetes and experiment with it

## ⚙️ Hardware

I'm hosting all my virtualized nodes in a custom built server made from old parts from my old gaming PC

| CPU      | RAM   | OS           |
| -------- | ----- | ------------ |
| 16 cores | 64GiB | Proxmox VE 9 |

## 🖥️ Nodes

All nodes were deployed with a Cloud-Init template

| Type   | CPU     | RAM  | OS        |
| ------ | ------- | ---- | --------- |
| Server | 2 cores | 2GiB | Debian 13 |
| Server | 2 cores | 2GiB | Debian 13 |
| Server | 2 cores | 2GiB | Debian 13 |
| Agent  | 4 cores | 8GiB | Debian 13 |
| Agent  | 4 cores | 8GiB | Debian 13 |
