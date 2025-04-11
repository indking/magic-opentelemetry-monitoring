```markdown
# 📘 Open Telemetry Dashboard Setup Documentation

This guide outlines the necessary prerequisites and step-by-step instructions to install, upgrade, and uninstall the `monitoring-stack` using a Helm chart.

---

## ✅ Prerequisites

Ensure the following components are installed and configured before proceeding with the setup:

- **Helm**
- **kubectl**
- **MicroK8s**

### MicroK8s Configuration

- Enable the following MicroK8s addons:
  ```bash
  microk8s enable dns storage metallb
  ```
- Configure **MetalLB** with **at least 5 free IPs** in your local network.
- Ensure **XPI** and **Kubernetes cluster nodes** are in the same network.

### GHCR (GitHub Container Registry) Access

- Ensure you have a **GitHub account**.
- Authenticate with **GHCR** before pulling or pushing Helm charts.

---

## 🔐 Login to GHCR

Authenticate Helm to interact with GHCR:

```bash
echo <pat_key> | helm registry login ghcr.io --username <username> --password-stdin
```

Replace `<username>` with your GitHub username and `<pat_key>` with your GitHub Personal Access Token (PAT).

---

## 🚀 Installation from GHCR

Install the chart from GitHub Container Registry:

```bash
helm install monitoring-stack oci://ghcr.io/indking/charts/monitoring-stack --version <version> --namespace monitoring --create-namespace
```

The current version is `0.1.2`. To install the latest package, use:

```bash
helm install monitoring-stack oci://ghcr.io/indking/charts/monitoring-stack --version 0.1.2 --namespace monitoring --create-namespace
```

---

## ⬆️ Upgrade Chart Version

To upgrade the `monitoring-stack` to a newer version:

```bash
helm upgrade monitoring-stack oci://ghcr.io/indking/charts/monitoring-stack --version <latest-version> --namespace monitoring
```

---

## 🧹 Uninstallation

To remove the `monitoring-stack`:

```bash
helm uninstall monitoring-stack --namespace monitoring
```

⚠️ **Note**: This does not delete the `monitoring` namespace.

To delete the namespace as well, run:

```bash
kubectl delete namespace monitoring
```
