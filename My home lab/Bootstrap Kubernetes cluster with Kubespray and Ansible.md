1. Install Ansible
2. Install containerd
3. Install Kubespay
4. Create a container image from the upstream kubespray image
	1. Create a git repo to contain the CI/CD eventually used to create clusters
	2. Create an `images/kubespray` subdirectory
	3. Create a `Containerfile` within subdirectory that extends Kubespray image
	4. Create `build` script to build and push to preferred registry
5. Create cluster with container
6. Install k8sapps

## Tips and caveats

- Kubespray *will* destructively change the hostname of all target nodes.
- Kubespray officially cannot upgrade more than one minor version (2.24.1 -> 2.25.1)
- Kubespray repo is *not* required to use the container image installation method (just create `inventory`).
- While Kubespray supports installation of NVIDIA device plugin it assume defaults that differ from what others might want in their deployments of both Node Feature Discovery (label filters, for example) and device plugin labels and annotations. For this reason many will prefer to keep these both as k8sapps.
- Remove the `spec.taints` if creating a single-node cluster
- Don't forget to [harden](https://github.com/kubernetes-sigs/kubespray/blob/master/docs/operations/hardening.md).



