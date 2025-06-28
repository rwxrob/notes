Here is a summary of my home lab setup.

## Considerations

- Rocky linux (Redhat) for all virtual machines since same as work
- Ubuntu and Alpine for all containers

## Hardware

- HPZ640 refurbished (56 core, 126 gb)

## Kubernetes

- Build all clusters with Kubespray custom Ansible playbook

### Bastion machine / Infrastructure cluster

- Primary get-shit-done Linux machine
- Ubuntu since easiest to manage
- Doubles as bastion gateway host
- Single-node cluster
- 12 cores, 16 gb

### Production cluster

- Three control planes (2 cores, 8 gb)
- Two worker nodes (2 cores, 16 gb)

### Development cluster

- Three control planes (2 cores, 8 gb)
- Two worker nodes (2 cores, 16 gb)
