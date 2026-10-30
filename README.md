<!-- DOCSIBLE START -->
# Ansible Role: role_containerd


role_containerd to install containerd


## Table of Contents

- [Requirements](#requirements)
- [Dependencies](#dependencies)
- [Role Variables](#role-variables)
- [Task Overview](#task-overview)
- [Example Playbook](#example-playbook)
- [Documentation Maintenance](#documentation-maintenance)
- [License](#license)
- [Author Information](#author-information)

## Requirements



- Ansible >= 2.9


- Supported platforms:
  - AlmaLinux (7, 8, 9)



## Dependencies


This role requires the following roles and collections:




  
    
  

  
    
  

  
    
  

  
    
  



**Roles:**

- [role_base](https://github.com/ginanck/role_base.git) (version: master)




**Collections:**

- `community.docker` (>= 4.8.1)

- `community.general` (>= 6.6.1)

- `ansible.posix` (>= 1.5.4)



To install all dependencies:
```bash
ansible-galaxy install -r meta/install_requirements.yml
```


## Role Variables

**These are static variables with lower priority**



#### File: defaults/main.yml

| Var | Type | Value |
|-----|------|-------|
| [containerd_apply_sysctl](defaults/main.yml#L107) | bool | `True` |
| [containerd_arch_map](defaults/main.yml#L25) | dict |  |
| [containerd_arch_map.aarch64](defaults/main.yml#L28) | str | `arm64` |
| [containerd_arch_map.amd64](defaults/main.yml#L27) | str | `amd64` |
| [containerd_arch_map.arm64](defaults/main.yml#L29) | str | `arm64` |
| [containerd_arch_map.ppc64le](defaults/main.yml#L30) | str | `ppc64le` |
| [containerd_arch_map.riscv64](defaults/main.yml#L32) | str | `riscv64` |
| [containerd_arch_map.s390x](defaults/main.yml#L31) | str | `s390x` |
| [containerd_arch_map.x86_64](defaults/main.yml#L26) | str | `amd64` |
| [containerd_architecture](defaults/main.yml#L34) | str | `<multiline value: folded_strip>` |
| [containerd_binary_checksum](defaults/main.yml#L71) | str |  |
| [containerd_binary_checksums](defaults/main.yml#L79) | dict |  |
| [containerd_binary_install_path](defaults/main.yml#L42) | str | `/usr/local/bin` |
| [containerd_binary_link_path](defaults/main.yml#L44) | str | `/usr/local/bin` |
| [containerd_binary_staging_path](defaults/main.yml#L43) | str | `/opt/containerd` |
| [containerd_checksum_algorithm](defaults/main.yml#L70) | str | `sha256` |
| [containerd_cni_bin_dir](defaults/main.yml#L60) | str | `/opt/cni/bin` |
| [containerd_cni_conf_dir](defaults/main.yml#L61) | str | `/etc/cni/net.d` |
| [containerd_cni_plugins_checksum](defaults/main.yml#L73) | str |  |
| [containerd_cni_plugins_checksums](defaults/main.yml#L81) | dict |  |
| [containerd_cni_plugins_version](defaults/main.yml#L17) | str | `1.7.1` |
| [containerd_config_disabled_plugins](defaults/main.yml#L50) | list |  |
| [containerd_config_file](defaults/main.yml#L47) | str | `/etc/containerd/config.toml` |
| [containerd_config_systemd_cgroup_enabled](defaults/main.yml#L49) | bool | `True` |
| [containerd_config_version](defaults/main.yml#L48) | str | `{{ '3' if containerd_version is version('2.0.0', '>=') else '2' }}` |
| [containerd_crictl_config_file](defaults/main.yml#L136) | str | `/etc/crictl.yaml` |
| [containerd_crictl_debug](defaults/main.yml#L135) | bool |  |
| [containerd_crictl_image_endpoint](defaults/main.yml#L133) | str | `{{ containerd_crictl_runtime_endpoint }}` |
| [containerd_crictl_runtime_endpoint](defaults/main.yml#L132) | str | `/run/containerd/containerd.sock` |
| [containerd_crictl_timeout](defaults/main.yml#L134) | int | `10` |
| [containerd_crictl_version](defaults/main.yml#L18) | str | `1.32.0` |
| [containerd_kernel_modules](defaults/main.yml#L86) | list |  |
| [containerd_kernel_modules.0](defaults/main.yml#L87) | str | `overlay` |
| [containerd_kernel_modules.1](defaults/main.yml#L88) | str | `br_netfilter` |
| [containerd_modules_load_file](defaults/main.yml#L89) | str | `/etc/modules-load.d/containerd.conf` |
| [containerd_registry_config_dir](defaults/main.yml#L114) | str | `/etc/containerd/certs.d` |
| [containerd_registry_config_path](defaults/main.yml#L115) | str | `{{ containerd_registry_config_dir }}` |
| [containerd_registry_mirrors](defaults/main.yml#L124) | dict |  |
| [containerd_runc_checksum](defaults/main.yml#L72) | str |  |
| [containerd_runc_checksums](defaults/main.yml#L80) | dict |  |
| [containerd_runc_version](defaults/main.yml#L16) | str | `1.3.0` |
| [containerd_sandbox_image](defaults/main.yml#L127) | str | `registry.k8s.io/pause:3.10` |
| [containerd_service_binary_path](defaults/main.yml#L45) | str | `/usr/local/bin` |
| [containerd_setup_type](defaults/main.yml#L8) | str | `repo` |
| [containerd_sysctl_conf_file](defaults/main.yml#L91) | str | `99-containerd.conf` |
| [containerd_sysctl_parameters](defaults/main.yml#L92) | list |  |
| [containerd_sysctl_parameters.0](defaults/main.yml#L93) | dict |  |
| [containerd_sysctl_parameters.0.name](defaults/main.yml#L93) | str | `net.ipv4.ip_forward` |
| [containerd_sysctl_parameters.0.value](defaults/main.yml#L94) | int | `1` |
| [containerd_sysctl_parameters.1](defaults/main.yml#L95) | dict |  |
| [containerd_sysctl_parameters.1.name](defaults/main.yml#L95) | str | `net.ipv6.conf.all.forwarding` |
| [containerd_sysctl_parameters.1.value](defaults/main.yml#L96) | int | `1` |
| [containerd_sysctl_parameters.2](defaults/main.yml#L97) | dict |  |
| [containerd_sysctl_parameters.2.name](defaults/main.yml#L97) | str | `net.bridge.bridge-nf-call-iptables` |
| [containerd_sysctl_parameters.2.value](defaults/main.yml#L98) | int | `1` |
| [containerd_sysctl_parameters.3](defaults/main.yml#L99) | dict |  |
| [containerd_sysctl_parameters.3.name](defaults/main.yml#L99) | str | `net.bridge.bridge-nf-call-ip6tables` |
| [containerd_sysctl_parameters.3.value](defaults/main.yml#L100) | int | `1` |
| [containerd_sysctl_parameters.4](defaults/main.yml#L101) | dict |  |
| [containerd_sysctl_parameters.4.name](defaults/main.yml#L101) | str | `vm.swappiness` |
| [containerd_sysctl_parameters.4.value](defaults/main.yml#L102) | int |  |
| [containerd_systemd_service_file](defaults/main.yml#L57) | str | `/etc/systemd/system/containerd.service` |
| [containerd_version](defaults/main.yml#L15) | str | `2.1.0` |




## Task Overview


This role performs the following tasks:


### File: `tasks/kernel.yml`

| Task Name | Module | Has Conditions | Line |
|-----------|--------|----------------|------|
| [ensure modules-load.d exists](tasks/kernel.yml#L) | ansible.builtin.file | No | N/A |
| [persist required kernel modules](tasks/kernel.yml#L) | ansible.builtin.template | No | N/A |
| [load required kernel modules in the current boot](tasks/kernel.yml#L) | community.general.modprobe | No | N/A |
| [ensure /etc/sysctl.d exists](tasks/kernel.yml#L) | ansible.builtin.file | No | N/A |
| [create sysctl configuration file for containerd](tasks/kernel.yml#L) | ansible.builtin.template | No | N/A |
| [apply sysctl parameters to the running kernel](tasks/kernel.yml#L) | ansible.builtin.command | Yes | N/A |




### File: `tasks/registry.yml`

| Task Name | Module | Has Conditions | Line |
|-----------|--------|----------------|------|
| [create registry configuration directory](tasks/registry.yml#L) | ansible.builtin.file | Yes | N/A |
| [create per-registry configuration directories](tasks/registry.yml#L) | ansible.builtin.file | Yes | N/A |
| [install registry CA certificates](tasks/registry.yml#L) | ansible.builtin.copy | Yes | N/A |
| [render per-registry hosts.toml](tasks/registry.yml#L) | ansible.builtin.template | Yes | N/A |




### File: `tasks/post-tasks.yml`

| Task Name | Module | Has Conditions | Line |
|-----------|--------|----------------|------|
| [create containerd config directory](tasks/post-tasks.yml#L) | ansible.builtin.file | No | N/A |
| [get latest crictl release version without token](tasks/post-tasks.yml#L) | ansible.builtin.uri | Yes | N/A |
| [get latest crictl release version with token](tasks/post-tasks.yml#L) | ansible.builtin.uri | Yes | N/A |
| [set crictl_latest from appropriate source](tasks/post-tasks.yml#L) | ansible.builtin.set_fact | Yes | N/A |
| [set crictl version from release data](tasks/post-tasks.yml#L) | ansible.builtin.set_fact | Yes | N/A |
| [use the pinned crictl version](tasks/post-tasks.yml#L) | ansible.builtin.set_fact | Yes | N/A |
| [setup crictl binary for repo installation type](tasks/post-tasks.yml#L) | ansible.builtin.include_tasks | Yes | N/A |
| [render registry mirror and host configuration](tasks/post-tasks.yml#L) | ansible.builtin.include_tasks | No | N/A |
| [detect installed containerd version](tasks/post-tasks.yml#L) | ansible.builtin.command | No | N/A |
| [set config version from the installed binary](tasks/post-tasks.yml#L) | ansible.builtin.set_fact | Yes | N/A |
| [create containerd configuration file](tasks/post-tasks.yml#L) | ansible.builtin.template | No | N/A |
| [create crictl configuration file](tasks/post-tasks.yml#L) | ansible.builtin.template | No | N/A |
| [install containerd systemd service for binary installs](tasks/post-tasks.yml#L) | ansible.builtin.template | Yes | N/A |
| [ensure containerd service is enabled and running](tasks/post-tasks.yml#L) | ansible.builtin.systemd | No | N/A |




### File: `tasks/prerequisites.yml`

| Task Name | Module | Has Conditions | Line |
|-----------|--------|----------------|------|
| [ensure containerd binaries are in PATH](tasks/prerequisites.yml#L) | ansible.builtin.template | No | N/A |




### File: `tasks/main.yml`

| Task Name | Module | Has Conditions | Line |
|-----------|--------|----------------|------|
| [Install Prerequisite Packages](tasks/main.yml#L) | ansible.builtin.include_tasks | No | N/A |
| [Prepare the kernel (persistent modules and sysctls)](tasks/main.yml#L) | ansible.builtin.include_tasks | No | N/A |
| [Setup Containerd runtime](tasks/main.yml#L) | ansible.builtin.include_tasks | No | N/A |
| [Setup Containerd Configuration](tasks/main.yml#L) | ansible.builtin.include_tasks | No | N/A |




### File: `tasks/binary/resolve-checksums.yml`

| Task Name | Module | Has Conditions | Line |
|-----------|--------|----------------|------|
| [resolve containerd checksum from an explicit pin](tasks/binary/resolve-checksums.yml#L) | ansible.builtin.set_fact | Yes | N/A |
| [resolve containerd checksum from the per-architecture map](tasks/binary/resolve-checksums.yml#L) | ansible.builtin.set_fact | Yes | N/A |
| [fetch the published containerd checksum file](tasks/binary/resolve-checksums.yml#L) | ansible.builtin.get_url | Yes | N/A |
| [read the published containerd checksum](tasks/binary/resolve-checksums.yml#L) | ansible.builtin.slurp | Yes | N/A |
| [set containerd checksum from the published file](tasks/binary/resolve-checksums.yml#L) | ansible.builtin.set_fact | Yes | N/A |
| [resolve runc checksum from an explicit pin](tasks/binary/resolve-checksums.yml#L) | ansible.builtin.set_fact | Yes | N/A |
| [resolve runc checksum from the per-architecture map](tasks/binary/resolve-checksums.yml#L) | ansible.builtin.set_fact | Yes | N/A |
| [fetch the published runc checksum file](tasks/binary/resolve-checksums.yml#L) | ansible.builtin.get_url | Yes | N/A |
| [read the published runc checksum](tasks/binary/resolve-checksums.yml#L) | ansible.builtin.slurp | Yes | N/A |
| [set runc checksum from the published file](tasks/binary/resolve-checksums.yml#L) | ansible.builtin.set_fact | Yes | N/A |
| [resolve cni plugins checksum from an explicit pin](tasks/binary/resolve-checksums.yml#L) | ansible.builtin.set_fact | Yes | N/A |
| [resolve cni plugins checksum from the per-architecture map](tasks/binary/resolve-checksums.yml#L) | ansible.builtin.set_fact | Yes | N/A |
| [fetch the published cni plugins checksum file](tasks/binary/resolve-checksums.yml#L) | ansible.builtin.get_url | Yes | N/A |
| [read the published cni plugins checksum](tasks/binary/resolve-checksums.yml#L) | ansible.builtin.slurp | Yes | N/A |
| [set cni plugins checksum from the published file](tasks/binary/resolve-checksums.yml#L) | ansible.builtin.set_fact | Yes | N/A |




### File: `tasks/binary/setup-cni-plugins.yml`

| Task Name | Module | Has Conditions | Line |
|-----------|--------|----------------|------|
| [download cni plugins archive with checksum verification](tasks/binary/setup-cni-plugins.yml#L) | ansible.builtin.get_url | No | N/A |
| [create cni directories](tasks/binary/setup-cni-plugins.yml#L) | ansible.builtin.file | No | N/A |
| [extract cni plugins](tasks/binary/setup-cni-plugins.yml#L) | ansible.builtin.unarchive | No | N/A |




### File: `tasks/binary/setup-containerd.yml`

| Task Name | Module | Has Conditions | Line |
|-----------|--------|----------------|------|
| [download containerd archive with checksum verification](tasks/binary/setup-containerd.yml#L) | ansible.builtin.get_url | No | N/A |
| [extract containerd archive](tasks/binary/setup-containerd.yml#L) | ansible.builtin.unarchive | No | N/A |
| [find extracted containerd binaries](tasks/binary/setup-containerd.yml#L) | ansible.builtin.find | No | N/A |
| [install containerd binaries into the path the unit uses](tasks/binary/setup-containerd.yml#L) | ansible.builtin.copy | No | N/A |




### File: `tasks/binary/set-download-urls.yml`

| Task Name | Module | Has Conditions | Line |
|-----------|--------|----------------|------|
| [set download URLs and filenames for each component](tasks/binary/set-download-urls.yml#L) | ansible.builtin.set_fact | No | N/A |




### File: `tasks/binary/set-releases.yml`

| Task Name | Module | Has Conditions | Line |
|-----------|--------|----------------|------|
| [set default version variables if not defined](tasks/binary/set-releases.yml#L) | ansible.builtin.set_fact | No | N/A |
| [get latest releases from GitHub API for binary versions without token](tasks/binary/set-releases.yml#L) | ansible.builtin.uri | Yes | N/A |
| [get latest releases from GitHub API for binary versions with token](tasks/binary/set-releases.yml#L) | ansible.builtin.uri | Yes | N/A |
| [parse and set versions (use latest stable from GitHub)](tasks/binary/set-releases.yml#L) | ansible.builtin.set_fact | Yes | N/A |
| [set version variables for items with predefined versions](tasks/binary/set-releases.yml#L) | ansible.builtin.set_fact | Yes | N/A |




### File: `tasks/binary/setup-runc.yml`

| Task Name | Module | Has Conditions | Line |
|-----------|--------|----------------|------|
| [download runc binary with checksum verification](tasks/binary/setup-runc.yml#L) | ansible.builtin.get_url | No | N/A |




### File: `tasks/binary/main.yml`

| Task Name | Module | Has Conditions | Line |
|-----------|--------|----------------|------|
| [pin the binary install path used by the rendered unit](tasks/binary/main.yml#L) | ansible.builtin.set_fact | No | N/A |
| [create binary staging and install directories](tasks/binary/main.yml#L) | ansible.builtin.file | No | N/A |
| [Set Release Versions](tasks/binary/main.yml#L) | ansible.builtin.import_tasks | No | N/A |
| [Set Download URLs](tasks/binary/main.yml#L) | ansible.builtin.import_tasks | No | N/A |
| [Resolve and verify artifact checksums](tasks/binary/main.yml#L) | ansible.builtin.import_tasks | No | N/A |
| [Setup Containerd](tasks/binary/main.yml#L) | ansible.builtin.import_tasks | No | N/A |
| [Setup Runc](tasks/binary/main.yml#L) | ansible.builtin.import_tasks | No | N/A |
| [Setup CNI Plugins](tasks/binary/main.yml#L) | ansible.builtin.import_tasks | No | N/A |




### File: `tasks/repo/RedHat.yml`

| Task Name | Module | Has Conditions | Line |
|-----------|--------|----------------|------|
| [set repository distribution name](tasks/repo/RedHat.yml#L) | ansible.builtin.set_fact | No | N/A |
| [install dnf-plugins-core (RedHat family)](tasks/repo/RedHat.yml#L) | ansible.builtin.dnf | No | N/A |
| [download docker repository file (RedHat family)](tasks/repo/RedHat.yml#L) | ansible.builtin.get_url | No | N/A |
| [check if containernetworking-plugins package is available](tasks/repo/RedHat.yml#L) | ansible.builtin.command | No | N/A |
| [set packages to install for RedHat](tasks/repo/RedHat.yml#L) | ansible.builtin.set_fact | No | N/A |
| [install containerd.io package](tasks/repo/RedHat.yml#L) | ansible.builtin.dnf | No | N/A |




### File: `tasks/repo/Debian.yml`

| Task Name | Module | Has Conditions | Line |
|-----------|--------|----------------|------|
| [set repository distribution name](tasks/repo/Debian.yml#L) | ansible.builtin.set_fact | No | N/A |
| [install prerequisites (Debian family)](tasks/repo/Debian.yml#L) | ansible.builtin.apt | No | N/A |
| [create keyrings directory (Debian family)](tasks/repo/Debian.yml#L) | ansible.builtin.file | No | N/A |
| [check if docker gpg key exists](tasks/repo/Debian.yml#L) | ansible.builtin.stat | No | N/A |
| [add docker gpg key (Debian family)](tasks/repo/Debian.yml#L) | ansible.builtin.apt_key | Yes | N/A |
| [check if docker repository exists](tasks/repo/Debian.yml#L) | ansible.builtin.stat | No | N/A |
| [add docker repository (Debian family)](tasks/repo/Debian.yml#L) | ansible.builtin.apt_repository | Yes | N/A |
| [install containerd.io package](tasks/repo/Debian.yml#L) | ansible.builtin.apt | No | N/A |




### File: `tasks/repo/crictl.yml`

| Task Name | Module | Has Conditions | Line |
|-----------|--------|----------------|------|
| [create containerd bin dir](tasks/repo/crictl.yml#L) | ansible.builtin.file | No | N/A |
| [extract crictl](tasks/repo/crictl.yml#L) | ansible.builtin.unarchive | No | N/A |
| [check if versioned crictl binary exists](tasks/repo/crictl.yml#L) | ansible.builtin.stat | No | N/A |
| [install crictl to version-specific path](tasks/repo/crictl.yml#L) | ansible.builtin.copy | Yes | N/A |
| [calculate priority from version](tasks/repo/crictl.yml#L) | ansible.builtin.set_fact | No | N/A |
| [set up alternatives for crictl binaries](tasks/repo/crictl.yml#L) | community.general.alternatives | No | N/A |
| [remove rootless setup scripts](tasks/repo/crictl.yml#L) | ansible.builtin.file | No | N/A |
| [find containerd binary path](tasks/repo/crictl.yml#L) | ansible.builtin.command | No | N/A |
| [set default containerd path](tasks/repo/crictl.yml#L) | ansible.builtin.set_fact | No | N/A |




### File: `tasks/repo/main.yml`

| Task Name | Module | Has Conditions | Line |
|-----------|--------|----------------|------|
| [Install containerd.io package](tasks/repo/main.yml#L) | ansible.builtin.include_tasks | No | N/A |






## Example Playbook

```yaml
---
- hosts: all
  become: yes
  roles:
    - role: role_containerd

      vars:
        containerd_setup_type: repo
        containerd_version: 2.1.0
        containerd_runc_version: 1.3.0

```

## License


license (GPL-2.0-or-later, MIT, etc)


## Author Information


**Author:** gkorkmaz




**GitHub:** [gkorkmaz](https://github.com/gkorkmaz)

---
*This documentation was automatically generated using [docsible](https://github.com/zbohm/docsible).*
<!-- DOCSIBLE END -->
