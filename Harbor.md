TODO

1. Determine is the highest level of Harbor supported by k8s 1.32.5
2. Update Harbor k8s app from Helm chart for target version
3. Create additional manifest for one-off special application

Latest Harbor version: v2.13.1-rc3
Supported k8s version: v1.20+ (per https://github.com/goharbor/harbor-helm)
Bitnami Helm chart: 26.7.10

- Discovered that pinned <14 of postgresql version is now removed (which was bug)