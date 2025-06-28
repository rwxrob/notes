1. Install Ansible
2. Install Kubespay
3. Create a container with kubespray
	1. Create a git repo to contain the CI/CD eventually used to create clusters
	2. Create an `images/kubespray` subdirectory
	3. Create a `Containerfile` within subdirectory that extends Kubespray image
	4. Create `build` script to build and push to preferred registry
4. Create cluster with container
5. Install k8sapps