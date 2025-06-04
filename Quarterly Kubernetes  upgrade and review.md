This document outlines a consistent strategy for ensuring an on-prem, in-house, enterprise Kubernetes cluster with its k8sapps is kept up to date and reviewed for improvements and security once a quarter. Ideally, a enterprise K8S operations team would simply follow this checklist of tasks.

## Assumptions and requirements

- Kubespray
- Configuration management in simple git repo
- Ansible Automation Platform for node/machine creation (managed by infra team)
- Ansible playbooks repo for Kubernetes cluster creation and modification
- k8sapp spec 2.0
- Ansible playbooks for node creation
