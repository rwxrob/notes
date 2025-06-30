- Kubespray
- Vault

Stuff installed by Kubespray:
- Calico (`kube_network_plugin`)
- Containerd (`container_manager`)
- `kubeadm`
- `kubectl`
- `kubelet`

Required by Kubernetes (k8sapps):

- k8s.app.security
- k8s.app.external-secrets
- k8s.app.metallb
- k8s.app.istio
- k8s.app.node-feature-discovery
- k8s.app.nvidia-device-plugin
- k8s.app.lws
- k8s.app.kyverno
- k8s.app.metrics-server
- k8s.app.vpa
- k8s.app.storage
- k8s.app.prometheus
- k8s.app.elastic-agent
- k8s.app.kubespray-operator
- 

Provide services (k8sapps):

- ElasticSearch (eck, beats, etc.)
- Grafana
- Kyverno
- Harbor
- Mkdocs (user-facing)
- Mkdocs (internal)
- Tekton?

