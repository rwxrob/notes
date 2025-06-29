1. Get current versions of all supported k8s clusters
2. Identify Kubespray version that supports oldest current k8s cluster version (which may not be latest)
3. Upgrade Kubespray to newest version that support oldest k8s cluster
4. 
## Tips and caveats

- OS updates must be done *before* Kubespray is run (or optional `system-upgrade` playbook)
- Kubespray drops support for old k8s versions (no backward compatibility promise, see release notes)
- Clusters deployed with newer Kubespray and incompatible with clusters deployed with older Kubespray
- Kubespray depends on `kubeadm` to do cert renewal and will rotate so long as don't fall to far behind