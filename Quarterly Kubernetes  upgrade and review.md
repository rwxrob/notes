This document outlines a consistent strategy for ensuring an on-prem, in-house, enterprise Kubernetes cluster with its k8sapps is kept up to date and reviewed for improvements and security once a quarter. Ideally, a enterprise K8S operations team would simply follow this checklist of tasks.

## Assumptions and requirements

- Configuration management in simple git repo
- RedHat Ansible Automation Platform for node/machine creation (managed by infra team)
- Custom Ansible playbooks (not RedHat) for Kubernetes cluster creation and modification
- Kubespray for both infra and k8s
- Configuration management in simple git repo
- k8sapp spec 2.0
- Limit scope of k8sapps to those required and supported by team (Istio, MetalLB, Harbor, Nvidia Device Plugin, etc.)
- Only upgrade to minor versions n-1 (1.23 -> 1.31)
## Procedures

- 
- For each k8sapp:
	- Check for compatibility with planned k8s version
	- Identify any breaking changes to existing apps that depend on k8sapps
	- Update k8sapp to latest k8sapp specification
