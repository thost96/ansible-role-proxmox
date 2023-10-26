# ansible-role-proxmox
Ansible Role for Proxmox PVE Server configuration and Tools

## Features
* Disable Proxmox Subscription Warning
* Disable Enterprise Repository
* Enable no-subscription Repository
* InfluxDB and Graphite Metric Server configuration

### Planned Features / in Developement:
* System Apt and Kernel Upgrades incl. old Kernel cleanup
* ZFS / Cockpit Install and Setup
* LLDP Install
* InfluxDB Metrics using HTTP/HTTPS
* Postfix Mail Alert Configuration
* ZFS Latency Monitoring
* PVE Network Configuration

All Fetures are tested and working with Proxmox version 7.x and 8.x.

## Role Variables

Available variables are listed below, along with default values (see `defaults/main.yml`):

### Proxmox Subscription Warning

    disable_subscription_popup: true

If PVE Subscrition Warning Popup should be removed or not.

### Enterprise Repository

    disable_enterprise_repo: true

Disable PVE Enterprise Repository when no license is installed or leave it enabled (license required). 

### Enable no-subscription Repository

    enable_no_subscription_repo: true

Enable PVE no Subscription Repository (no Proxmox licsense required). 

### PVE System Upgrades

    system_upgrades: false

If enabled, Proxmox Server APT Updates will automatically installed and old packages removed. 

### Influx Metrics

    metrics_influx: false

Enable Metric Server Support for InfluxDB. The following two options then must be specified:

    metrics_influx_server: influx

IP Address or Hostname of InfluxDB Server. 

    metrics_influx_port: 8089

Port used by InfluxDB Server.

### Graphite Metrics

    metrics_graphite: false

Enable Metric Server Support for Graphite. The following two options then must be specified:

    metrics_graphite_server: graphite

IP Address or Hostname of Graphite Server. 

    metrics_graphite_port: 2003

Port used by Graphite Server.

### System Upgrades

    system_upgrades: false

    system_kernel_upgrade: false

    system_kernel_clean: false


### Tools 

#### Cockpit as ZFS UI

    tools_cockpit: false

If enabled, Cockpit with ZFS Manager Plugin will be installed to manage ZFS from UI on Port 9090. 

## Example Playbook

### Use default values

    - hosts: all
      roles:
        - role: thost96.proxmox

### Enable InfluxDB Metrics

    - hosts: all
      vars:
        metrics_influx: true
        metrics_influx_server: influx
        metrics_influx_port: 8089
      roles:
        - role: thost96.proxmox

### Enable Graphite Metrics

    - hosts: all
      vars:
        metrics_graphite: true
        metrics_graphite_server: graphite
        metrics_graphite_port: 2003
      roles:
        - role: thost96.proxmox

## License

MIT / BSD
