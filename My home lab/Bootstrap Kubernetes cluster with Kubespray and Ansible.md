1. Install Ansible
2. Install Kubespay
3. Create a container image from the upstream kubespray image
	1. Create a git repo to contain the CI/CD eventually used to create clusters
	2. Create an `images/kubespray` subdirectory
	3. Create a `Containerfile` within subdirectory that extends Kubespray image
	4. Create `build` script to build and push to preferred registry
4. Create cluster with container
5. Install k8sapps

## Tips and caveats

- Kubespray *will* destructively change the hostname of all target nodes
- The entire Kubespray repo is *not* required to use the container image installation method (just create `inventory`)
- OS package updates must be done *before* Kubespray is run (or can be run with the optional `system-upgrade` playbook)
- Kubespray *does* remove old k8s versions (see release notes)
- Kubespray depends on `kubeadm` to do cert renewal but has disabled option to do it outside