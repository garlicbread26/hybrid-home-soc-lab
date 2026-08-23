# Hybrid Home SOC Lab

A hands-on hybrid Security Operations Center (SOC) lab combining a local virtualized security environment with Oracle Cloud Infrastructure.

## What I Built

```text
Windows Host
     |
VMware Workstation Pro
     |
   pfSense
   ├── Suricata
   ├── pfBlockerNG
   └── Guest VLAN
          |
    Ubuntu Desktop
    Test / Defender

        Tailscale VPN
        CGNAT Bypass
              |
           OCI VCN
          /       \
 Ubuntu CLI      Wazuh
    |             |
Kali/Docker      SIEM

SOC-HOME-LAB/
│
├── README.md
│
├── 01-Architecture/
│   ├── topology.md
│   ├── network-diagram.png
│   └── ip-addressing.md
│
├── 02-Network/
│   ├── pfsense.md
│   ├── vlans.md
│   ├── firewall-rules.md
│   └── tailscale.md
│
├── 03-Virtualization/
│   ├── vmware.md
│   └── virtual-machines.md
│
├── 04-Cloud/
│   ├── oci.md
│   ├── networking.md
│   └── wazuh-deployment.md
│
├── 05-Wazuh/
│   ├── installation.md
│   ├── agents.md
│   ├── rules.md
│   ├── dashboards.md
│   └── syslog.md
│
├── 06-Detection/
│   ├── windows-events.md
│   ├── linux-events.md
│   ├── authentication.md
│   └── network-events.md
│
├── 07-Investigation/
│   ├── incident-01.md
│   ├── incident-02.md
│   └── incident-03.md
│
├── 08-Troubleshooting/
│   ├── wazuh-connectivity.md
│   ├── oci-ip-change.md
│   └── routing.md
│
└── screenshots/
