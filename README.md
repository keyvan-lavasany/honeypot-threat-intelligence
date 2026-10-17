# Honeypot Threat Intelligence

A centralized honeypot monitoring service designed to collect, aggregate, and visualize attacker activity across multiple data centers using Cowrie, Promtail, Loki, and Grafana.

## Overview

Honeypot Threat Intelligence provides centralized visibility into activity observed by distributed SSH honeypot sensors. It uses Cowrie to capture interactions with exposed SSH services, Promtail to collect and forward container logs, Loki to aggregate and query logs, and Grafana to visualize activity through monitoring dashboards.

The project focuses on maintaining a consistent, manageable configuration for honeypot sensors and the central monitoring stack.

## Architecture

The service consists of two main components:

### 1. Distributed Honeypot Sensors

Sensors are deployed across multiple data centers. Each sensor runs:

- **Cowrie:** An SSH/Telnet honeypot that records attacker interactions and login attempts.
- **Promtail:** Collects Cowrie container logs and forwards them to the central Loki instance.

### 2. Central Monitoring Stack

A central server hosts the logging and visualization components:

- **Loki:** Centralized log aggregation, storage, and querying.
- **Grafana:** Dashboards and visual exploration of collected logs.

### Data Flow

```text
Distributed Data Centers
          |
          v
    Cowrie Honeypot
          |
          v
        Promtail
          |
          v
    Central Loki
          |
          v
       Grafana
```

## Technology Stack

| Component | Purpose |
|---|---|
| Cowrie | SSH/Telnet honeypot and interaction logging |
| Promtail | Log collection and forwarding |
| Loki | Centralized log aggregation and querying |
| Grafana | Monitoring dashboards and visualization |
| Docker Compose | Container deployment and service configuration |
| Git | Configuration versioning and change tracking |

## Repository Structure

- `sensor compose file.yml` — Docker Compose configuration for honeypot sensors.
- `sensor promtail config.yml` — Promtail configuration for collecting and forwarding sensor logs.
- `central server compose file.yml` — Docker Compose configuration for the central monitoring stack.
- `central loki config.yml` — Loki configuration.
- `.gitignore` — Excludes documentation, images, runtime data, and selected local or sensitive files from Git tracking.

## Key Capabilities

- Centralized collection of honeypot logs from multiple data centers.
- Visibility into SSH login attempts and attacker interactions.
- Log querying and visualization through Loki and Grafana.
- Consistent, version-controlled deployment configurations.
- A foundation for further threat analysis and security monitoring improvements.

## Deployment Notes

The project uses Docker Compose to define the sensor and central monitoring services.

Before deployment:

1. Ensure Docker and Docker Compose are available on the target hosts.
2. Configure the sensor's Promtail settings to reach the central Loki endpoint.
3. Verify that required configuration files are mounted at the paths expected by the Compose definitions.
4. Review exposed ports, network access, storage, and service permissions before deployment.
5. Confirm that logs are reaching Loki and can be queried through Grafana.

Deployment details may vary depending on the data center environment and network configuration.

## Security Considerations

- Restrict access to Loki and Grafana to trusted networks and authorized users.
- Review exposed ports and firewall rules on all hosts.
- Avoid committing credentials, access tokens, private keys, or other sensitive information.
- Keep container images and software components updated.
- Treat honeypot logs as untrusted data and handle them accordingly.

## Project Scope

This repository contains configuration and deployment resources for the honeypot logging and monitoring stack. It does not, by itself, provide automated incident response or guarantee the identification of malicious activity.

## License

No license has been specified yet.
