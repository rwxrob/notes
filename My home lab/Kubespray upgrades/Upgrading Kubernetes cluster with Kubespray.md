This document is intended for engineers responsible for production clusters that cannot easily be rebuilt or migrated without significant disruption or cost (e.g. clusters with GPU-bound ML workloads). It includes key caveats, guidance on managing upstream divergence.

Upgrading a Kubernetes cluster in-place using Kubespray is a deliberate, stepwise process. Kubespray enforces strict upgrade boundaries:

- Only one minor version upgrade at a time is supported
- Downgrades are not supported
- Versioning is non-semantic — any change may trigger a new Kubespray release
- Kubespray and Kubernetes versions are loosely coupled

> [!CAUTION]
> Because newer Kubespray versions no longer track Kubernetes component versions in `inventory`, upgrades require careful inspection of Dockerfiles, release notes, and source diffs. This is particularly important if *any* fork or changes to the Kubespray source itself have been incorporated into any cluster creation or upgrade workflows.

This procedure provides a clear and repeatable method to:

- Select the next valid Kubespray version
- Analyze potential impact from upstream changes
- Manage and commit the Kubespray submodule
- Build and tag updated Kubespray container images
- Reconcile changes to `inventory`
- Safely execute the upgrade and validate the result
## Evaluate

1. Determine the current Kubespray version
	1. `cd kubespray; gitl`
2. Determine the next minor Kubespray version (*never more than one, patch versions ok*)
	1. `cd kubespray; git tag -l`
3. Note any divergence/patches from upstream
4. Read the [release notes](https://github.com/kubernetes-sigs/kubespray/releases) for the planned version (potentially in team huddle)
	1. Determine if anything in release notes warrants further source code evaluation
		1. `git diff --name-only v2.24.1 v2.25.1 -- inventory galaxy.yml playbooks roles`
		2. Same as above but without `--name-only` to inspect *all* changes
	2. If k8s, calico, or containerd version bump, evaluate release notes for those as well
5. Prepare a report summarizing relevant changes and considerations for PR review
## Execute

1. Pull the next minor Kubespray version tag into the `kubespray` submodule
	1. `cd *kubespray; git checkout tags/v2.25.1`
	2. `cd ..; git add *kubespray; git commit -m 'bump kubespray to v2.25.1'
2. Update the upstream `kubespray` image tag and build/push new `kubespray` image
	1. `cd images/*kubespray`
	2. Update `Containerfile` (or `Dockerfile`) to have version tag matching submodule
	3. Update `build` script to have own updated tag
	4. Build and push it with build script
	5. Update cluster creation and upgrade scripts with new extended container image tag
3. Understand and merge any changes from `inventory/sample` into current `inventory`
	1. `diff -r inventory kubespray/inventory/sample`
	2. Consider just copying `inventory/sample` and applying customizations so future diffs are more relevant
	3. Be very careful here because the Kubespray project has a history of *not* updating the sample to be consistent with how the `kube_version` is derived causing it to force a back-level k8s version because setting it overrides the kubelet checksum version look method.
	4. Also be careful that the actual content of the *current* inventory matches the fields and format and structure of the `inventory/sample` that was originally copied to create your own inventory (names have changed, fields have changed, Kubernetes version must be updated explicitly, etc.)
4. Run the [upgrade playbook](https://github.com/kubernetes-sigs/kubespray/blob/master/docs/operations/upgrades.md#multiple-upgrades)

## Validate

1. Login to node and run `kubelet --version`
2. Note that `kubectl get no -A` may not immediately show current version
3. Run all system/k8sapp regression tests
4. Inform customers and have them install apps and do their own testing
## Tips and caveats

- Kubespray cannot be used to regress a version.
- Kubespray depends on tags on the repos to communicate versions.
- Kubespray *only* supports upgrading [one minor version at a time](https://github.com/kubernetes-sigs/kubespray/blob/master/docs/operations/upgrades.md#multiple-upgrades).
- Kubernetes and Kubespray versions have nothing to do with one another.
- Kubespray minor versions are triggered from *any* change to k8s or other dependency.
- Kubespray doesn't follow semantic versioning (every version is "stable").
- Kubernetes component versions have been removed from Kubespray inventory in later versions.
- Kubespray project uses `master` branch for development.
- Kubespray Kubernetes version best determined by looking in `Dockerfile` for image.
## Versioning

>    Minor releases can change components' versions, but not the major kube_version. Greater kube_version requires a new major or minor release. For example, if Kubespray v2.0.0 is bound to kube_version: 1.4.x, calico_version: 0.22.0, etcd_version: 3.0.6, then Kubespray v2.1.0 may be bound to only minor changes to kube_version, like v1.5.1 and any changes to other components, like etcd v4, or calico 1.2.3. And Kubespray v3.x.x shall be bound to `kube_version: 2.x.x` respectively.

- PR with removal of versions from inventory and justification.
  https://github.com/kubernetes-sigs/kubespray/commit/985e4ebb23f66631bc8938324adcead2114955a3
## Questions

*What is a critical customer app does not work all all with the new cluster but the cluster already has other customers using it?*

We could create a new cluster at the version required by the customer application just for them until the problem is remediated. Or, we could adopt a blue/green architecture and they could stay on the "old" cluster until they are ready to move to the new one.

*How can I know if there is a Kubespray update?*

Best way is to check the tags on the Kubespray repo for new ones.

*Why not just build a new cluster at a given version instead of upgrading?*

Because people are already using the current cluster and would all have to move into the new cluster and the ML GPU resources are too expensive to not use fully during the migration. This makes the risk of breaking something by doing an in-place upgrade more palatable to management.