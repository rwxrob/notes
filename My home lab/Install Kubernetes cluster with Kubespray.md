> [!WARNING]
> This is my way of creating a Kubernetes environment that mirrors what we have at work. It may not be the best way for you.

This procedure can be followed initially to create the first cluster and resource from which to build the cluster or it can be used to create an additional cluster simply by updating things in these steps—primarily the inventory.

1. Setup an admin machine from which to run Ansible/Kubespray playbooks
	1. Setup ssh
		1. Install if not already there
		2. Create key pair
	2. Install Podman (if not already there)
2. Setup one or more RedHat (Rocky) machine(s) to become Kubernetes nodes
	1. Give distinct DNS names
	2. Disable any firewalls
		1. `sudo systemctl disable firewalld`
	3. Optionally snapshot base after OS install for rollback if virtual machines
3. Configure admin machine to have ssh password-less key access to future k8s nodes
	1. `ssh-copy-id NODENAME` (not IP)
4. Create a git repo with code for cluster creation
	1. Create a GitHub repo
		1. `gh repo create k8s.cicd`
	2. Add the upstream Kubespray repo as a submodule
		1. Change into the new repo
			1. `cd k8s.cicd`
		2. Fork the upstream Kubespray repo and clone
			1. `gh repo fork kubernetes-sigs/kubespray --clone`
			2. `git submodule add ./kubespray`
			3. `git submodule summary`
	3. Extend the Kubespray image
		1. Create an `images/kubespray` directory
		2. Change into `images/kubespray` directory
		3. Create a `Containerfile` that extends Kubespray image
		4. Create `build` script to build and push to preferred registry
	4. Create or update the inventory
		1. Create `inventory` directory if it does not exist
5. Create or update the inventory
	1. If first time, copy the upstream Kubespray submodule `inventory/sample` directory
		1. `cp -r kubespray/inventory/sample inventory`
	2. Update the inventory file with machine names (not IPs) to become Kubernetes nodes
		1. `vi inventory/inventory.ini`
6. Extend the container image as desired
	1. Create a subdirectory for images with `kubespray` image
		1. `mkdir -p images/kubespray
	2. Create a `Containerfile` that extends upstream image
		1. `cd images/kubespray`
		2. `touch Containerfile`
		3. `echo 'FROM quay.io/kubespray/kubespray:v2.28.0' >> Containerfile`
		4. Add `RUN` line updating and 
		5. installing any additional tools needed
			```Containerfile
			FROM quay.io/kubespray/kubespray:v2.28.0
			LABEL org.opencontainers.image.source https://github.com/rwxrob/k8s.cicd
			
			RUN --mount=type=cache,target=/var/cache/apt,sharing=locked \
			  apt-get update -q && \
			  apt-get install -yq --no-install-recommends \
			  dnsutils
			
			# TODO: gradually add that stuff necessary to pull down the k8sapps
			```
		5. Create and run `build` script locally on admin machine
			```bash
			#!/bin/bash
			set -e
			image=ghcr.io/rwxrob/k8s.cicd/kubespray:v0.0.2
			podman build -t "$image" --format docker .
			#podman push "$image"
			```
7. Create a `create-cluster` script to run the Kubespray Ansible playbook
	1. `cd k8s.cicd`
	2. `n=create-cluster; touch $n; chmod +x $n`
	3. Copy the initial Quick Start -> Docker script from `kubespray/README.md`and customize
		```bash
		#!/bin/bash
		#image="quay.io/kubespray/kubespray:v2.28.0"
		image="ghcr.io/rwxrob/k8s.cicd/kubespray:v0.0.2"
		podman run --rm -it \
			--mount type=bind,source="$(pwd)"/inventory,dst=/inventory \
			--mount type=bind,source="${HOME}"/.ssh/id_ed25519,dst=/root/.ssh/id_ed25519 \
			"$image" ansible-playbook -b -K -i /inventory/inventory.ini \
			--private-key /root/.ssh/id_ed25519 cluster.yml
		```
8. Run and debug `create-cluster` script
	1. `./create-cluster`
9. Validate created cluster
	1. Login to any newly create k8s node
	2. Become root
		1. `sudo su -`
	3. List all current nodes
		1. `kubectl get no -A`
	4. Make sure pods are running
		1. `kubectl get pod -A`

----
1. Install vault into its own virtual machine (simulated vault service provider outside of my management)
2. Install Harbor container registry k8sapp into management cluster
3. Install k8sapps

## Tips and caveats

- Kubespray *will* destructively change the hostname of all target nodes.
- Kubespray officially cannot upgrade more than one minor version (2.24.1 -> 2.25.1)
- Kubespray repo is *not* required to use the container image installation method (just create `inventory`).
- While Kubespray supports installation of NVIDIA device plugin it assume defaults that differ from what others might want in their deployments of both Node Feature Discovery (label filters, for example) and device plugin labels and annotations. For this reason many will prefer to keep these both as k8sapps.
- Remove the `spec.taints` if creating a single-node cluster
- Don't forget to [harden](https://github.com/kubernetes-sigs/kubespray/blob/master/docs/operations/hardening.md).



