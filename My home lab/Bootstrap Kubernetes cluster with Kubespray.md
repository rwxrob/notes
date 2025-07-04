> [!WARNING]
> This is my way of creating a Kubernetes environment that mirrors what we have at work.

1. Identify a jump host from which to run Ansible/Kubespray playbooks
2. Install podman
3. Create a container image from the upstream kubespray image
	1. Create a git repo to contain the CI/CD eventually used to create clusters (ex: `k8s.cicd`)
	2. Create an `images/kubespray` subdirectory
	3. Create a `Containerfile` within subdirectory that extends Kubespray image
	4. Create `build` script to build and push to preferred registry
4. Create cluster with container
5. Install k8sapps

## Tips and caveats

- Kubespray *will* destructively change the hostname of all target nodes.
- Kubespray officially cannot upgrade more than one minor version (2.24.1 -> 2.25.1)
- Kubespray repo is *not* required to use the container image installation method (just create `inventory`).
- While Kubespray supports installation of NVIDIA device plugin it assume defaults that differ from what others might want in their deployments of both Node Feature Discovery (label filters, for example) and device plugin labels and annotations. For this reason many will prefer to keep these both as k8sapps.
- Remove the `spec.taints` if creating a single-node cluster
- Don't forget to [harden](https://github.com/kubernetes-sigs/kubespray/blob/master/docs/operations/hardening.md).



