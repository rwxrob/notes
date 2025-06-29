## 📊 How to Determine Installed CNI Plugin and Version with Kubespray

Use these steps to generate a reliable report of which CNI plugin is installed by Kubespray and what version is in use.

---

### ✅ Step 1: Identify the Installed CNI Plugin

Open the following file:

```
inventory/<your-cluster>/group_vars/k8s_cluster/k8s_cluster.yml
```

Look for:

```yaml
kube_network_plugin: calico  # or flannel, cilium, etc.
```

This value determines which CNI plugin Kubespray actually installs.

---

### ✅ Step 2: Check the Version from Downloads

Open:

```
roles/downloads/defaults/main.yml
```

Search for the matching variable based on the plugin name:

- `calico_version`
- `flannel_version`
- `cilium_version`
- etc.

This shows the default version Kubespray installs unless overridden elsewhere.

---

### ✅ Step 3: Confirm from the Live Cluster (Optional)

Run:

```bash
kubectl get pods -n kube-system
```

Then, for example, if using Calico:

```bash
kubectl get daemonset -n kube-system calico-node -o jsonpath='{.spec.template.spec.containers[0].image}'
```

This gives the actual running image, which should match the version from `downloads.yml`.

---

## 📝 Sample Report Entry

```markdown
### Networking (CNI)
- Plugin: **Calico**
- Version: **v3.25.0** _(from `downloads.yml`)_
- Confirmed running: ✅ via `kubectl get pods -n kube-system`

### Source:
- `k8s_cluster.yml` → `kube_network_plugin: calico`
- `downloads.yml` → `calico_version: v3.25.0`
```

---

Let me know if you want a script to automate this as a CI/CD audit step or compliance check.
