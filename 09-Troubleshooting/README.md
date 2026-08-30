# 09 · Troubleshooting & Connectivity

## Overview

During the deployment of the SOC automation stack, connectivity between the Ubuntu host, Docker bridge network, n8n container and Wazuh server required troubleshooting.

The issue initially appeared as an n8n connectivity failure even though the n8n container itself was running.

---

## Environment

| Component | Address / Network |
|---|---|
| Ubuntu n8n VM | `192.168.20.100` |
| Wazuh Server | `192.168.20.100` |
| n8n | TCP `5678` |
| Docker bridge | `172.17.0.0/16` |
| Docker bridge gateway | `172.17.0.1` |
| n8n container | `172.17.0.2` |

---

## Problem

The n8n container was running and Docker showed the port mapping:

```text
0.0.0.0:5678->5678/tcp
