This document outlines a consistent strategy for ensuring an on-prem, in-house, enterprise Kubernetes cluster with its k8sapps is kept up to date and reviewed for improvements and security once a quarter. Ideally, a enterprise K8S operations team would simply follow this checklist of tasks.

## Assumptions and requirements

- Configuration management in simple git repo
- RedHat Ansible Automation Platform for node/machine creation (managed by infra team)
- Custom Ansible playbooks calling Kubespray for Kubernetes cluster creation and modification
- Ansible versions for infra and k8s *not* in synch (to allow Kubespray updates independently)
- Configuration management in simple git repo
- k8sapp spec 2.0
- Limit scope of k8sapps to those required and supported by team (Istio, MetalLB, Harbor, Nvidia Device Plugin, etc.)
- Only upgrade to minor versions n-1 (1.23 -> 1.31)
- Blue/green evaluated and proved too expensive given number of high-cost GPUs involved
## Procedures

- Build target upgraded cluster and all k8sapps in new cluster to allow customer testing

- For each k8sapp:
	- Check for compatibility with planned k8s version
	- Check that the k8sapp resource and code is the same as what is currently in cluster
	- Identify any breaking changes to existing apps that depend on k8sapps
	- Communicate all changes to customers *before* upgrade
	- Update k8sapp to latest k8sapp specification
	- If k8sapp from Helm chart:
		- Create branch/draft pr
		- Run `build` on latest
		- Run `git diff` to see changes and assess impact to apps that use it

## Related

- https://akuity.io/blog/the-rendered-manifests-pattern
- 
