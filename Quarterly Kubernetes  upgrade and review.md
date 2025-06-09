This document outlines a consistent strategy for ensuring an on-prem, in-house, enterprise Kubernetes cluster and its k8sapps are kept up to date and reviewed for improvements and security once a quarter. Ideally, a enterprise K8S operations team would simply follow this checklist of tasks.

## Assumptions and requirements

- Configuration management in simple git repo
- RedHat Ansible Automation Platform for node/machine creation (managed by infra team)
- Custom Ansible playbooks calling Kubespray for Kubernetes cluster creation and modification
- Ansible versions for infra and k8s *not* in synch (to allow Kubespray updates independently)
- Configuration management in simple git repo
- k8sapp spec 2.0 (potentially 3.0)
- Limit scope of k8sapps to those required and supported by team (Istio, MetalLB, Harbor, Nvidia Device Plugin, etc.)
- Only upgrade to minor versions n-1 (1.23 -> 1.31)
## Procedures

- Research new Kubernetes version
	- Are there any breaking changes or deprecations?
		- Documented changes
		- Undocumented changes (source code diff perhaps)
	- Can this be done as in-place upgrade?
- Build new cluster and k8sapps versions and test for breakages
	- Spin up a new sandbox cluster at targeted version with existing core k8sapps (kubespray)
	- Validate that core k8sapps are working (regression test scripts, benchmarking, etc.)
	- For each core k8sapp:
		- Check for compatibility with planned k8s version
		- Check that the k8sapp resource and code is the same as what is currently in cluster
			- Update k8sapp to latest k8sapp specification
			- If k8sapp from Helm chart:
				- Create branch/draft pr
				- Run `build` on latest
				- Run `git diff` to see changes and assess impact to apps that use it
				- Identify any potential breaking changes to existing customer apps that depend on k8sapps
					- If the namespace has the `prod`
				- Address breaking changes and assess need to communicate to customers
	- Update `kubectl`
	- Update `klogin`
- Allow customers to test their apps
	- Audit customer contact information to ensure up to date (moves, latest emails, etc.)
	- Invite customers to test apps on new cluster with new core k8sapps
	- Await completion and validation of all customer testing
- Update and practice disaster recovery for new cluster and k8sapps
- Move new cluster and k8sapps into production

## Related

- https://akuity.io/blog/the-rendered-manifests-pattern

## Questions for discussion

- Are we going to entertain an in-place upgrade?
- Do we even want our customers to test their apps *before* deploying latest cluster and core k8sapps?
- Can we even spend the money on an even a single H100 in sandbox just long-term testing?
- Can we even have customers truly test their apps if they require H100 to even try?
- What if we scheduled time blocks for customers to test with limited H100 capacity in sandbox?
- Could we get through all customers testing within a safe time frame to maintain quarterly upgrades?
- Can we stagger k8sapp upgrades every two quarters (or whatever)?

## Conclusions and recommendations

- Recommend blue/green on whatever cycle we can hit
	- Most like what we just did
	- Tooling for migration applies
	- Requires H100s in both clusters but not "sandbox" so easier to justify
	- Allows customers to migrate at their leisure within a specific time frame
	- Eliminates need to migrate from sandbox to "production" since sandbox *is* production