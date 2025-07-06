1. Note the current Kubespray Kubernetes version (`kube_version`)
2. Note the current version of Kubespray
## Tips and caveats

- Kubespray *only* supports upgrading one minor version at a time.
- Kubernetes and Kubespray versions have nothing to do with one another.
- Kubespray major and minor releases are bound to a given `kube_version`.
- Kubespray doesn't follow semantic versioning (every version is "stable").
- ***Kubespray grabs the latest k8s version unless specified explicitly.***
- Kubernetes version `kube_version` **does not exist** anywhere in Kubespray source repo.
## Versioning

>    Minor releases can change components' versions, but not the major kube_version. Greater kube_version requires a new major or minor release. For example, if Kubespray v2.0.0 is bound to kube_version: 1.4.x, calico_version: 0.22.0, etcd_version: 3.0.6, then Kubespray v2.1.0 may be bound to only minor changes to kube_version, like v1.5.1 and any changes to other components, like etcd v4, or calico 1.2.3. And Kubespray v3.x.x shall be bound to `kube_version: 2.x.x` respectively.
## Questions

*What is a critical customer app does not work all all with the new cluster but the cluster already has other customers using it?*

We could create a new cluster at the version required by the customer application just for them until the problem is remediated. Or, we could adopt a blue/green architecture and they could stay on the "old" cluster until they are ready to move to the new one.