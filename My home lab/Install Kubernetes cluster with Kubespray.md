> [!WARNING]
> This is my way of creating a Kubernetes environment that mirrors what we have at work. It may not be the best way for you.

1. Identify a machine from which to run Ansible/Kubespray playbooks
2. Install podman (if not already there) (optionally snapshot)
3. Create a git repo with everything to create clusters via gitops ci/cd (ex: `k8s.cicd`)
	1. Extend the Kubespray image
		1. Create an `images/kubespray` subdirectory to extend base kubespray image
		2. Create a `Containerfile` within subdirectory that extends Kubespray image
		3. Create `build` script to build and push to preferred registry
	2. Create or update the inventory
		1. Create `inventory` directory if it does not exist
		
4. Create or identify one or more Redhat (Rocky) machines to become k8s nodes
5. Optionally snapshot future k8s node machines to enable rollback for practice
6. Update `k8s.cicd/inventory` with future k8s node *names*

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



