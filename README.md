# OpenTelemetry Loki to Prometheus Bridge 🌉

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Python Version](https://img.shields.io/badge/python-3.8%2B-blue)](https://www.python.org/downloads/)
[![Docker](https://img.shields.io/badge/docker-supported-blue)](https://www.docker.com/)
[![Kubernetes](https://img.shields.io/badge/kubernetes-supported-blue)](https://kubernetes.io/)

A powerful bridge that connects your Loki logs to Prometheus metrics, enabling seamless observability and monitoring of your applications.

![Architecture Overview](docs/images/architecture.png)

## 🚀 Features

- **Real-time Log Processing**: Continuously processes logs from Loki and converts them to Prometheus metrics
- **Flexible Metric Generation**: Customizable metric generation based on log patterns
- **Kubernetes Ready**: Native Kubernetes deployment support
- **Rich Monitoring**: Comprehensive metrics for server and project status
- **Robust Error Handling**: Detailed error tracking and reporting
- **Configurable**: Easy configuration through environment variables

## 📋 Prerequisites

- Python 3.8 or higher
- Docker/Podman
- Kubernetes cluster (for K8s deployment)
- Loki instance
- Prometheus instance

## 🛠️ Quick Start

1. **Clone the repository:**
   ```bash
   git clone https://github.com/indking/opentelemetry-loki-prometheus-bridge.git
   cd opentelemetry-loki-prometheus-bridge
   ```

2. **Set up environment variables:**
   ```bash
   cp .env.example .env
   # Edit .env with your configuration
   ```

3. **Build the Docker image:**
   ```bash
   # Linux
   ./build.sh
   
   # Windows
   build.bat
   ```

4. **Deploy to Kubernetes:**
   ```bash
   # Linux
   ./deploy-k8s.sh
   
   # Windows
   deploy-k8s.bat
   ```

## 🔧 Configuration

| Environment Variable | Description | Default |
|---------------------|-------------|---------|
| Loki_SERVER_HOST | Loki server hostname | 10.9.9.149 |
| Loki_SERVER_PORT | Loki server port | 3100 |
| PROMETHEUS_GATEWAY | Prometheus pushgateway URL | http://10.9.8.59:9091 |
| LOG_LEVEL | Logging level | INFO |
| MAX_WORKERS | Maximum worker threads | 10 |

## 📊 Metrics

### Server Metrics
- `project_name`: Name of the Project
- `current_session_start`: Current Session Start Time
- `latest_transaction_time`: Latest Transaction Time
- `uptime_current_session_ns`: Uptime in Nanoseconds
- `uptime_current_session_sec`: Uptime in Seconds

### Performance Metrics
- `total_errors_current_session`: Total Errors in Current Session
- `errors_last_hour`: Errors in Last Hour
- `total_flows_current_session`: Total Flows Executed
- `flows_last_hour`: Flows Executed in Last Hour

### Status Metrics
- `server_status`: Current Server Status
- `project_status`: Current Project Status
- `server_count`: Count of Servers

## 📈 Grafana Dashboard

![Grafana Dashboard](docs/images/grafana-dashboard.png)

Import our pre-configured Grafana dashboard for instant visualization of your metrics:
- Dashboard ID: `12345`
- [Download JSON](docs/dashboards/main-dashboard.json)

## 🔍 Monitoring Examples

### Server Status Monitoring
```promql
server_status{status="Running"}
```

### Error Rate Alert
```promql
rate(errors_last_hour[5m]) > 10
```

## 🤝 Contributing

We welcome contributions! Please see our [Contributing Guide](CONTRIBUTING.md) for details.

1. Fork the repository
2. Create your feature branch
3. Commit your changes
4. Push to the branch
5. Create a Pull Request

## 📝 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🙏 Acknowledgments

- OpenTelemetry Community
- Loki Team
- Prometheus Team
- All our contributors

## 📞 Support

- Create an [Issue](https://github.com/indking/opentelemetry-loki-prometheus-bridge/issues)
- Join our [Discord Community](https://discord.gg/your-invite)
- Email: support@example.com

## 🔮 Roadmap

- [ ] Support for additional log formats
- [ ] Enhanced metric customization
- [ ] Real-time alerting integration
- [ ] Multi-cluster support
- [ ] Machine learning for anomaly detection
