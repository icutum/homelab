# Homelab

## Overview

This is a GitOps [FluxCD](https://fluxcd.io/) based repository that manages my K3s Kubernetes cluster with each node virtualized through Proxmox.
It was deployed using the following Ansible playbook: https://github.com/k3s-io/k3s-ansible

---

## Quickstart

First install SOPS/Age on your package manager of choice:

```bash
$ sudo apt install sops age
```

Then generate an age key pair, which we will use later:

```bash
$ age-keygen -o ~/.config/sops/age/keys.txt
```

Install the Flux CLI:

```bash
$ curl -s https://fluxcd.io/install.sh | sudo bash
```

After that, run the bootstrap command:

```bash
$ flux bootstrap github \
  --token-auth \
  --owner=<github-username> \
  --repository=<repository-name> \
  --branch=main \
  --path=clusters/<cluster-name> \
  --personal
```

Then, in the cluster, create the secret that will store the key pair so Flux knows how to decode encrypted manifests:

```bash
$ kubectl create secret generic sops-age \
  --namespace=flux-system \
  --from-file=age.agekey=keys.txt
```

Finally, change the public key in the .sops.yaml file:
```bash
$ vi .sops.yaml
```

## Nodes

My cluster consists of three server nodes forming a HA etcd control plane (tainted with `NoSchedule`) and two agent nodes. 
All nodes were deployed with a Cloud-Init template, and their configuration can be seen in my Terraform repository: https://github.com/icutum/infra

---

## Security

Secrets are managed with [SOPS](https://getsops.io/) in combination with [age](https://github.com/FiloSottile/age) to encrypt the values in the repository and decrypt them during FluxCD reconciliation

---

## Automation

[Renovate](https://github.com/renovatebot/renovate) scans the repository and opens pull requests for new container image and Helm release versions
