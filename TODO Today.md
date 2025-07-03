- [x] Upgrade the kubespray image to latest and retest against existing node1
- [x] Decide what k8sapps will be on the management cluster
	- [x] What does Kubespray already install for us by default? (Calico, etc.)
	- [x] What are the required k8sapps that are required for customer apps to work? (Istio, etc.)
	- [x] What are the k8sapps that provide core services? (Harbor, etc.)
- [x] Define the "breaking lab" architecture
	- [x] Build `walt` login machine - Ubuntu 2.25
    - [x] Install OS (user `rwxrob` as root admin)
    - [x] Setup NFS `/s` mount
    - [x] Update `~/rwxrob` to be `/s/rwxrob`
    - [x] Setup `rwxrob` admin user
	- [x] Build `heisenberg` single-node management k8s cluster - Rocky 9.4
		- [x] Drop NFS mount for home directories
		- [ ] [Bootstrap Kubernetes cluster with Kubespray and Ansible](My%20home%20lab/Bootstrap%20Kubernetes%20cluster%20with%20Kubespray%20and%20Ansible.md)


- [ ] Document high-level steps to create and upgrade cluster
	- [ ] Create cluster from scratch
	- [ ] Create a cluster using GitOps and Kubespray from management cluster
	- [ ] Upgrade cluster using the management cluster
- [ ] Update custom Kubespray image to match current work version
- [ ] Install Kubernetes admin/inf cluster with Kubespray (without k8sapps)
- [ ] Create five VMs for "prod" k8s cluster
- [ ] Create five VMs for "sandbox" (test01) cluster
- [ ] Create a list of k8sapps needed and where they will live
- [ ] Create k8sapp repos for core services and system apps running in k8s clusters

----

- [ ] Call Spectrum
- [ ] Pay WV tolls
- [ ] Pay rent
- [ ] Complete and submit teeth/nose insurance claim

----

- [ ] Join the Satanic Temple
- [ ] Update NeoVim with Terraform linter and colors
- [ ] Add current cluster context to my PS1 CLI prompt
- [ ] Setup Ansible inventory and playbooks on `walt` (login machine)
- [ ] Add a list of great resources
  - [ ] Add https://docs.kolkhis.dev/linux/nfs
- [ ] Make an LLM and search engine that only crunches data sources that I provide
- [ ] Add Tripwire to OpenWRT on router
- [ ] Add ha-proxy to OpenWRT router
- [ ] Add keepalived to OpenWRT router