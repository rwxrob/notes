Here is a summary of my home lab setup.

## Considerations

- Rocky linux (Redhat) for all virtual machines since same as work
- Ubuntu and Alpine for all containers
- Entirely random hostnames to prevent opsec attacks

## Hardware

- HPZ640 refurbished (56 core, 126 gb)

## Software

- Proxmox
- Kubernetes
- Hashicorp Vault
### Bastion machine

- Primary get-shit-done Linux machine
- Ubuntu since easiest to manage
- Doubles as bastion gateway host
- Single-node cluster
- 12 cores, 16 gb
----
## Kubernetes

- Build all clusters with Kubespray custom Ansible playbook

### 

### Blue/Green clusters

- Three control planes (2 cores, 8 gb)
- Two worker nodes (2 cores, 16 gb)

### k8sapps

- Harbor container registry


