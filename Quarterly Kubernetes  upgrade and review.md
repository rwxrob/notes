This document outlines a consistent strategy for ensuring an on-prem, in-house, enterprise Kubernetes cluster with its k8sapps is kept up to date and reviewed for improvements and security once a quarter. Ideally, a enterprise K8S operations team would simply follow this checklist of tasks.

## Assumptions and requirements

- Configuration management in simple git repo
- Ansible Automation Platform for node/machine creation (managed by infra team)
- Custom Ansible playbooks (not RedHat) for Kubernetes cluster creation and modification
- Kubespray for both infra and k8s
- Configuration management in simple git repo
- k8sapp spec 2.0
