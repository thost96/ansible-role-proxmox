# ansible-role-proxmox
Ansible Role for Proxmox PVE Server configuration and Tools

[![Release](https://github.com/thost96/ansible-role-proxmox/actions/workflows/release.yml/badge.svg)](https://github.com/thost96/ansible-role-proxmox/actions/workflows/release.yml)
[![Lint](https://github.com/thost96/ansible-role-proxmox/actions/workflows/lint.yml/badge.svg)](https://github.com/thost96/ansible-role-proxmox/actions/workflows/lint.yml)
[![Molecule Lint and Test](https://github.com/thost96/ansible-role-proxmox/actions/workflows/molecule.yml/badge.svg)](https://github.com/thost96/ansible-role-proxmox/actions/workflows/molecule.yml)
![Ansible Role](https://img.shields.io/ansible/role/d/xxxx)


## Features
* Disable Proxmox Subscription Warning
* Disable Enterprise Repository
* Enable no-subscription Repository
* LLDP Install
* System APT Upgrades
* Cockpit UI Install including ZFS Tools

### Planned Features / in Developement
* InfluxDB and Graphite Metric Server configuration
* Kernel Upgrades incl. old Kernel cleanup
* InfluxDB Metrics using HTTP/HTTPS
* Postfix Mail Alert Configuration
* ZFS Latency Monitoring
* PVE Network Configuration
* LXC Template Download
* PVE DNS and Domain configuration

All Fetures are tested and working with Proxmox version 7.x and 8.x.

## Role Variables

Available variables are listed below, along with default values (see `defaults/main.yml`):

| Variable Name                 | Description                                                       | Default Value | Type    |
| ---                           | ---                                                               | :---:         | :---:   |
| disable_subscription_popup    | PVE Subscrition Warning Popup should be removed or not            | true          | boolean |
| disable_enterprise_repo       | Disable PVE Enterprise Repository when no license is installed    | true          | boolean |
| enable_no_subscription_repo   | Enable PVE no Subscription Repository                             | true          | boolean |
| system_upgrades               | Proxmox Server APT Updates will automatically installed and old packages removed  | false         | boolean |
|  tools_lldp | LLDP will be installed and activated at boot | false  | boolean |
| tools_cockpit | Cockpit with ZFS Manager Plugin will be installed to manage ZFS from UI on Port 9090 | false | boolean |
| metrics_influx | Enables Metric Server Support for InfluxDB. | false | boolean |
| metrics_influx_server | IP Address or Hostname of InfluxDB Server | influx | string |
| metrics_influx_port | Port used by InfluxDB Server. Defaults to `8089`| 8089 | int |
| metrics_graphite | Enables Metric Server Support for Graphite | false | boolean |
| metrics_graphite_server | IP Address or Hostname of Graphite Server | graphite | string |
| metrics_graphite_port | Port used by Graphite Server. Defaults to `2003` | 2003 | int |
| system_kernel_upgrade | If set to `true`, Debian/PVE Kernel will be updated | false | boolean |
| system_kernel_clean | If set to `true`, old and unused Debian/PVE Kernel will be removed. | false | boolean |
   
## Example Playbook

### Use default values

    - hosts: all
      roles:
        - role: thost96.proxmox

### Install Tools

    - hosts: all
      vars:
        tools_lldp: true
        tools_cockpit: true
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

## Version Schema

    <major>.<feature>.<fix>

* Major version can include breaking changes
* Feature version adds new Features
* Fix version are only smaller changes

## License

MIT / BSD
