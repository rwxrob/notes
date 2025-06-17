This document outlines a consistent strategy for ensuring an on-prem, in-house, enterprise Kubernetes cluster and its k8sapps are kept up to date and regularly reviewed for improvements and security.

## Handle Kubernetes upgrades

- For each Kubernetes component and core k8sapp:
    - Check if there is a new version available
    - Assess urgency of upgrading to new version
        - Can it wait until quarterly upgrade or later?
            - If yes:
                - Add to list of planner quarterly upgrades
                - End
            - Else:
                - Create story with relevant urgency
                - Assign to one or more admins:
                    - Upgrade k8sapp OR
                    - Upgrade Kubernetes
                - End


## Can it wait until quarterly or later?

If the answer is yes to the following then the upgrade can wait:

- Does the upgrade patch a critical security flaw?
- Is the new version > n-1?


- Is it newer than 
	- Identify the version targeted (n-1)
	- Are there immediate security concerns or requirements?
	- Are there any breaking changes or deprecations?
		- Documented changes
		- Undocumented changes (source code diff perhaps)
	- Can this be done as in-place upgrade?


## Upgrade k8sapp

TODO

## Upgrade kubernetes

TODO

## Work items

- Specify the `check` script or alternative

----

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
- Consider labeling additions, changes:
	- `system` - Istio, MetaLB, nvidia device plugin, node feature discover, etc.
	- `system`, `service` - Harbor, ArgoCD, Auth, MkDocs, etc.
## Notes

1. Immediately security upgrade
2. In-place upgrades (no migration needed)
3. Full cluster upgraded (all apps must be migrated)

What triggers an upgrade?
- Regularly reminder
- Event based or polling
- ~~Person on-call checking for version upgrades?~~ (won't get done)
- What about a regular polling system that generates a business event that triggers upgrade SOP:
	- What if we added `check` to the k8sapp v3 spec?
	- What if we added k8sapp that checks k8s cluster version releases and calls all `system` and `service` k8sapp `check` scripts?

# Idea for start up or open source project

- Create an application that can run as a standalone server, container, or k8sapp that simply checks the following and reports or calls a web-hook:
	- Check the current standard Kubernetes version
	- Check the current version of any k8sapp
	- Check other versions using any customizable check script
	- Make each check configurable using some "n-n" threshold for reporting
	- Regular intervals with email notifications and/or web page dashboard

1. Get the current version of kuberetes, capture to var
2. foreach k8sapp:
	1. pull down the `check` script from github
	2. run check script capturing version to var
3. Output JSON per JSON schema

