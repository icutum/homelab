# 🏠 Homelab

## 📕 Overview

This is a GitOps [FluxCD](https://fluxcd.io/) based repository that manages my K3s Kubernetes cluster with each node virtualized through Proxmox.
It was deployed using the following Ansible playbook: https://github.com/k3s-io/k3s-ansible

I'm currently building this homelab to learn Kubernetes and experiment with it

## ⚙️ Hardware

I'm hosting all my virtualized nodes in a custom built server made of parts from my old gaming PC

| CPU      | RAM   | OS           |
| -------- | ----- | ------------ |
| 16 cores | 64GiB | Proxmox VE 9 |

## 🖥️ Nodes

My cluster consists of three server nodes forming a HA etcd control plane (tainted with `NoSchedule`) and two agent nodes. 
All nodes were deployed with a Cloud-Init template

| Type   | CPU     | RAM  | OS        |
| ------ | ------- | ---- | --------- |
| Server | 2 cores | 4GiB | Debian 13 |
| Server | 2 cores | 4GiB | Debian 13 |
| Server | 2 cores | 4GiB | Debian 13 |
| Agent  | 4 cores | 8GiB | Debian 13 |
| Agent  | 4 cores | 8GiB | Debian 13 |

## 🔐 Security

Secrets are managed with [SOPS](https://getsops.io/) in combination with [age](https://github.com/FiloSottile/age) to encrypt the values in the repository, and decrypt them during FluxCD reconciliation

## 🤖 Automation

[Renovate](https://github.com/renovatebot/renovate) scans the repository and opens pull requests for new container image and Helm release versions

