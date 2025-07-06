1. Note the current version of Kubernetes
2. Note the current version of Kubespray
3. Look up the Kubespray version for the target (n-1) Kubernetes version
4. 
## Tips and caveats

- Kubespray *only* supports upgrading one minor version at a time.
- Kubernetes and Kubespray versions have nothing to do with one another
## Questions

*What is a critical customer app does not work all all with the new cluster but the cluster already has other customers using it?*

We could create a new cluster at the version required by the customer application just for them until the problem is remediated. Or, we could adopt a blue/green architecture and they could stay on the "old" cluster until they are ready to move to the new one.