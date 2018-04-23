# Ansible to configure and update ZTP server

Sample project using Ansible to setup and manage a ZTP server for use with Mellanox Oynx-based network switches.

In this project you'll find:
- (1) **A role to install all software on the remote server** with Playbooks and variables based on Ubuntu/Debian system.
- (2) Severals **ansible roles** packaged and documented into [Ansible roles](roles) to configure DHCP server and to deploy configuration files on all remote ZTP servers (FTP).
- (3) **[Examples of ZTP configurations](conf/ztp)** files.
- (4) **Playbook to play with ZTP roles** and update ZTP in a more complex project.
- (5) A simple example playbook to configures a Mellanox Oynx-based network switch post-ZTP boot up.



# 1. Ansible project to manage ZTP server

This project is managing the creation of a ZTP server running on a Debian like OS
- `ISC-DHCP-Server` is used as part of the DHCP server to provide IP address on the management network.
- `VSFTPd` is used to publish device's configuration and software packages.

All devices names, Ip addresses loopback addresses etc .. are defined in the [inventory file named "hosts"](hosts).

# 2. Playbooks

Available playbooks are listed below:
- [`playbook-ztp-setup`](playbook-ztp-setup.yml): Setup all softwares on a single or multiple ZTP servers (inc. isc-dhcp-server and vsftpd)
- [`playbook-ztp-init`](playbook-ztp-init.yml): Prepare a local configuration repository for configuration file creation and supporting files
- [`playbook-mlnx-oynx-conf-generate.yml`](playbook-mlnx--conf-generate.yml): Playbook to generate default configuration files for Mellanox Oynx network devices
- [`playbook-ztp-conf-generate`](playbook-ztp-conf-generate.yml): Create configuration for ZTP (specifically dhcpd.conf file) and store files on a local basis
- [`playbook-ztp-push-data`](playbook-ztp-push-data.yml): Push configuration files generated by `playbook-ztp-conf-generate` and supporting files to remote ztp server(s)
- [`playbook-ztp-complete`](`playbook-ztp-complete.yml`): Execute all the above actions in one playbook
- [`playbook-set-int-speed`](`playbook-set-int-speed.yml`): Example playbook which uses Mellanox Oynx network modules to do basic configuration of a switches booted using ZTP

# 3. Variables

All variables are stored in the  [hosts](hosts) file and [vars.yaml and ztp-variables.yaml](group_vars/all/). 

# 4. Contributing

Please refer to the file [CONTRIBUTING.md](CONTRIBUTING.md) for contribution guidelines.

# 5. Acknowledgement

This work is partially-based on initial work by titom73 ([GitHub respository](https://github.com/titom73/ansible-junos-ztp))