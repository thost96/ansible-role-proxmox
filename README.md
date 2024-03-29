# ansible-role-proxmox
Ansible Role for Proxmox PVE Server configuration and Tools

[![Release](https://github.com/thost96/ansible-role-proxmox/actions/workflows/release.yml/badge.svg)](https://github.com/thost96/ansible-role-proxmox/actions/workflows/release.yml)
[![Lint](https://github.com/thost96/ansible-role-proxmox/actions/workflows/lint.yml/badge.svg)](https://github.com/thost96/ansible-role-proxmox/actions/workflows/lint.yml)
[![Molecule Lint and Test](https://github.com/thost96/ansible-role-proxmox/actions/workflows/molecule.yml/badge.svg)](https://github.com/thost96/ansible-role-proxmox/actions/workflows/molecule.yml)

## Features
* Disable Proxmox Subscription Warning
* Disable Enterprise Repository
* Enable no-subscription Repository
* LLDP Install
* Proxmox Upgrades
* Cockpit UI Install including ZFS Tools
* Zamba LXC Toolbox Install
* Remove old installed Kernel versions

### Planned Features / in Developement
* InfluxDB and Graphite Metric Server configuration
* InfluxDB Metrics using HTTP/HTTPS
* Postfix Mail Alert Configuration
* ZFS Latency Monitoring
* PVE Network Configuration
* LXC Template Download
* PVE DNS and Domain configuration
* [PBS Post Installation Tasks](https://raw.githubusercontent.com/tteck/Proxmox/main/misc/post-pbs-install.sh)


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

If enabled, Proxmox Server Updates will automatically installed and old packages removed.

### Kernel cleanup

    system_kernel_clean: false

If set to `true`, old and unused Debian/PVE Kernel will be removed.

### Influx Metrics

    metrics_influx: false

Enables Metric Server Support for InfluxDB. The following two options then must be specified:

    metrics_influx_server: influx

IP Address or Hostname of InfluxDB Server.

    metrics_influx_port: 8089

Port used by InfluxDB Server. Defaults to `8089`.

### Graphite Metrics

    metrics_graphite: false

Enables Metric Server Support for Graphite. The following two options then must be specified:

    metrics_graphite_server: graphite

IP Address or Hostname of Graphite Server.

    metrics_graphite_port: 2003

Port used by Graphite Server. Defaults to `2003`.

### Tools

#### LLDP

    tools_lldp: false

If enabled, LLDP will be installed and activated at boot.

#### Cockpit as ZFS UI

    tools_cockpit: false

If enabled, Cockpit with ZFS Manager Plugin will be installed to manage ZFS from UI on Port 9090.

#### Zamba LXC Toolbox

    tools_zamba_lxc_toolbox: false

If enabled,  [Zamba LXC Toolbox](https://github.com/bashclub/zamba-lxc-toolbox) will be downloaded and default config generated.

(Optional): Default install Path is `/home/root/zamba-lxc-toolbox`. With `tools_zamba_lxc_toolbox_path` this can be changed.

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
        tools_zamba_lxc_toolbox: true
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

## Version Schema

    <major>.<feature>.<fix>

* Major version can include breaking changes
* Feature version adds new Features
* Fix version are only smaller changes

Changelog is available at [Changelog](changelog.md)

## License

MIT / BSD
