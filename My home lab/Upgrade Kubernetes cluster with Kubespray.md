> [!DANGER]
> Each upgrade using Kubespray *must* only be between one minor version and the procedure for each is sometimes *radically* different than the previous based on changes to the source, versioning, tagging, releasing, and other whims of project members. There is absolutely *zero* order in this chaos (at least enough to be procedurally executed or implemented in any sort of automation.)

1. Determine the current Kubespray version
2. Determine the current versions of everything Kubespray installed
3. Identify any custom changes (patches) to the Kubespray source diverting from upstream
4. Determine the next minor Kubespray version (***never more than one version***)
5. Study the new version to determine changes—especially to core components
## Tips and caveats

- Kubespray cannot be used to regress a version.
- Kubespray *only* supports upgrading one minor version at a time.
- Kubernetes and Kubespray versions have nothing to do with one another.
- Kubespray minor versions are triggered from *any* change to k8s or other dependency.
- Kubespray doesn't follow semantic versioning (every version is "stable").
- ***Kubespray grabs the latest k8s version unless specified explicitly.***
- Kubernetes component versions have been removed from Kubespray inventory.
- Kubespray project uses `master` branch for development.
- Kubespray Kubernetes version best determined by looking in `Dockerfile` for image.
## Versioning

>    Minor releases can change components' versions, but not the major kube_version. Greater kube_version requires a new major or minor release. For example, if Kubespray v2.0.0 is bound to kube_version: 1.4.x, calico_version: 0.22.0, etcd_version: 3.0.6, then Kubespray v2.1.0 may be bound to only minor changes to kube_version, like v1.5.1 and any changes to other components, like etcd v4, or calico 1.2.3. And Kubespray v3.x.x shall be bound to `kube_version: 2.x.x` respectively.

- PR with removal of versions from inventory and justification.
  https://github.com/kubernetes-sigs/kubespray/commit/985e4ebb23f66631bc8938324adcead2114955a3
## Questions

*What is a critical customer app does not work all all with the new cluster but the cluster already has other customers using it?*

We could create a new cluster at the version required by the customer application just for them until the problem is remediated. Or, we could adopt a blue/green architecture and they could stay on the "old" cluster until they are ready to move to the new one.