1. Get current versions of all supported k8s clusters
2. Identify Kubespray version that supports oldest current k8s cluster version (which may not be latest)
3. 

## Tips and caveats

- OS updates must be done *before* Kubespray is run (or optional `system-upgrade` playbook)
- Kubespray drops support for remove old k8s versions (see release notes)
- When extending kubespray image must maintain  for each supported Kubernetes version
- Kubespray depends on `kubeadm` to do cert renewal and will rotate so long as don't fall to far behind