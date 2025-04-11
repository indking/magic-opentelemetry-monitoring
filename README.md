# Magic OpenTelemetry Monitoring 🎯
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Helm](https://img.shields.io/badge/Helm-v3-blue)](https://helm.sh)
[![MicroK8s](https://img.shields.io/badge/MicroK8s-Latest-orange)](https://microk8s.io)

> A comprehensive OpenTelemetry monitoring stack for Kubernetes clusters using Helm.

## 📑 Table of Contents
- [Features](#-features)
- [Prerequisites](#-prerequisites)
- [Quick Start](#-quick-start)
- [Detailed Setup](#-detailed-setup)
  - [MicroK8s Configuration](#microk8s-configuration)
  - [GHCR Authentication](#ghcr-authentication)
- [Usage Guide](#-usage-guide)
  - [Installation](#installation)
  - [Upgrade](#upgrade)
  - [Uninstallation](#uninstallation)
- [Architecture](#-architecture)
- [Magic xpi OpenTelemetry Configuration](#magic-xpi-opentelemetry-configuration)

## ✨ Features
- Complete OpenTelemetry monitoring solution
- Easy deployment using Helm charts
- Integrated with MicroK8s
- Real-time metrics and monitoring
- Scalable architecture

## 🔧 Prerequisites

Before you begin, ensure you have the following tools installed:

| Tool | Version | Description |
|------|---------|-------------|
| [Helm](https://helm.sh/docs/intro/install/) | v3+ | Package manager for Kubernetes |
| [kubectl](https://kubernetes.io/docs/tasks/tools/) | Latest | Kubernetes command-line tool |
| [MicroK8s](https://microk8s.io/) | Latest | Lightweight Kubernetes |

## 🚀 Quick Start

```bash
# 1. Enable required MicroK8s addons
microk8s enable dns storage metallb

# 2. Login to GHCR
echo <pat_key> | helm registry login ghcr.io --username <username> --password-stdin

# 3. Install the monitoring stack
helm install monitoring-stack oci://ghcr.io/indking/charts/monitoring-stack \
  --version 0.1.2 \
  --namespace monitoring \
  --create-namespace
```

## 📖 Detailed Setup

### MicroK8s Configuration

1. Enable required addons:
   ```bash
   microk8s enable dns storage metallb
   ```

2. Requirements:
   - MetalLB configured with minimum 5 free IPs in local network
   - XPI and Kubernetes cluster nodes in the same network
   - Sufficient resources for monitoring components

### GHCR Authentication

1. Create a [GitHub Personal Access Token (PAT)](https://github.com/settings/tokens)
2. Authenticate with GHCR:
   ```bash
   echo <pat_key> | helm registry login ghcr.io --username <username> --password-stdin
   ```

## 🔨 Usage Guide

### Installation

```bash
# Latest version (0.1.2)
helm install monitoring-stack oci://ghcr.io/indking/charts/monitoring-stack \
  --version 0.1.2 \
  --namespace monitoring \
  --create-namespace
```

### Upgrade

```bash
helm upgrade monitoring-stack oci://ghcr.io/indking/charts/monitoring-stack \
  --version <latest-version> \
  --namespace monitoring
```

### Uninstallation

```bash
# Remove the monitoring stack
helm uninstall monitoring-stack --namespace monitoring

# Optional: Delete the namespace
kubectl delete namespace monitoring
```

## 🏗 Architecture

The monitoring stack consists of:
- OpenTelemetry Collector
- Prometheus
- Grafana
- AlertManager
- Other supporting components

## Magic xpi OpenTelemetry Configuration

To configure Magic xpi for OpenTelemetry:

1. Log in to Magic Monitor with admin credentials
2. Navigate to Settings -> Admin Settings
3. Under "OpenTelemetry Settings" section:
   - Select "gRPC" as the exporter type
   - Configure the collector endpoint URL (default: `http://<otel-collector-External-IP>:4317`)
     Note: You will receive the External IP address after the Helm chart installation completes
4. Save your configuration
5. Verify data collection:
   - Open Grafana portal (default: `http://<Grafana-External-IP>:3000`)
   - Navigate to the "OpenTelemetry Monitor Prom Live" dashboard
   - Confirm that metrics are being received

### Viewing and Analyzing Logs
You can view activity logs through the Grafana portal:
1. Navigate to the Grafana UI
2. Click on "Explore" in the left sidebar
3. Select "Loki" as your data source
4. Use LogQL to query and filter your logs
---

Thank you.

<div align="center">
Made with ❤️ by the Magic Monitoring Team
</div>
