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
| [containerd_binary_link_path](defaults/main.yml#L14) | str | `/usr/bin` |
| [containerd_config_disabled_plugins](defaults/main.yml#L19) | list |  |
| [containerd_config_file](defaults/main.yml#L17) | str | `/etc/containerd/config.toml` |
| [containerd_config_systemd_cgroup_enabled](defaults/main.yml#L18) | bool | `True` |
| [containerd_crictl_config_file](defaults/main.yml#L41) | str | `/etc/crictl.yaml` |
| [containerd_crictl_debug](defaults/main.yml#L40) | bool |  |
| [containerd_crictl_image_endpoint](defaults/main.yml#L38) | str | `{{ containerd_crictl_runtime_endpoint }}` |
| [containerd_crictl_runtime_endpoint](defaults/main.yml#L37) | str | `/run/containerd/containerd.sock` |
| [containerd_crictl_timeout](defaults/main.yml#L39) | int | `10` |
| [containerd_service_binary_path](defaults/main.yml#L15) | str | `/opt/containerd/bin` |
| [containerd_setup_type](defaults/main.yml#L12) | str | `repo` |
| [containerd_sysctl_conf_file](defaults/main.yml#L28) | str | `99-containerd.conf` |
| [containerd_sysctl_parameters](defaults/main.yml#L29) | list |  |
| [containerd_sysctl_parameters.0](defaults/main.yml#L30) | dict |  |
| [containerd_sysctl_parameters.0.name](defaults/main.yml#L30) | str | `net.ipv4.ip_forward` |
| [containerd_sysctl_parameters.0.value](defaults/main.yml#L31) | int | `1` |
| [containerd_sysctl_parameters.1](defaults/main.yml#L32) | dict |  |
| [containerd_sysctl_parameters.1.name](defaults/main.yml#L32) | str | `net.ipv6.conf.all.forwarding` |
| [containerd_sysctl_parameters.1.value](defaults/main.yml#L33) | int | `1` |
| [containerd_sysctl_parameters.2](defaults/main.yml#L34) | dict |  |
| [containerd_sysctl_parameters.2.name](defaults/main.yml#L34) | str | `vm.swappiness` |
| [containerd_sysctl_parameters.2.value](defaults/main.yml#L35) | int |  |
| [containerd_systemd_service_file](defaults/main.yml#L26) | str | `/etc/systemd/system/containerd.service` |




## Task Overview


This role performs the following tasks:


### File: `tasks/post-tasks.yml`

| Task Name | Module | Has Conditions | Line |
|-----------|--------|----------------|------|
| [create containerd config directory](tasks/post-tasks.yml#L) | ansible.builtin.file | No | N/A |
| [get latest crictl release version without token](tasks/post-tasks.yml#L) | ansible.builtin.uri | Yes | N/A |
| [get latest crictl release version with token](tasks/post-tasks.yml#L) | ansible.builtin.uri | Yes | N/A |
| [set crictl_latest from appropriate source](tasks/post-tasks.yml#L) | ansible.builtin.set_fact | No | N/A |
| [set crictl version from release data](tasks/post-tasks.yml#L) | ansible.builtin.set_fact | Yes | N/A |
| [setup crictl binary for repo installation type](tasks/post-tasks.yml#L) | ansible.builtin.include_tasks | Yes | N/A |
| [create containerd configuration file](tasks/post-tasks.yml#L) | ansible.builtin.template | No | N/A |
| [create crictl configuration file](tasks/post-tasks.yml#L) | ansible.builtin.template | No | N/A |
| [install containerd systemd service](tasks/post-tasks.yml#L) | ansible.builtin.template | No | N/A |
| [restart containerd service](tasks/post-tasks.yml#L) | ansible.builtin.systemd | Yes | N/A |




### File: `tasks/prerequisites.yml`

| Task Name | Module | Has Conditions | Line |
|-----------|--------|----------------|------|
| [ensure containerd binaries are in PATH](tasks/prerequisites.yml#L) | ansible.builtin.template | No | N/A |
| [ensure /etc/sysctl.d exists](tasks/prerequisites.yml#L) | ansible.builtin.file | No | N/A |
| [create sysctl configuration file for containerd](tasks/prerequisites.yml#L) | ansible.builtin.template | No | N/A |
| [apply sysctl parameters](tasks/prerequisites.yml#L) | ansible.builtin.command | Yes | N/A |




### File: `tasks/main.yml`

| Task Name | Module | Has Conditions | Line |
|-----------|--------|----------------|------|
| [Install Prerequisite Packages](tasks/main.yml#L) | ansible.builtin.include_tasks | No | N/A |
| [Setup Containerd runtime](tasks/main.yml#L) | ansible.builtin.include_tasks | No | N/A |
| [Setup Containerd Configuration](tasks/main.yml#L) | ansible.builtin.include_tasks | No | N/A |




### File: `tasks/binary/setup-cni-plugins.yml`

| Task Name | Module | Has Conditions | Line |
|-----------|--------|----------------|------|
| [download cni plugins binary file](tasks/binary/setup-cni-plugins.yml#L) | ansible.builtin.get_url | No | N/A |
| [download cni plugins verification file](tasks/binary/setup-cni-plugins.yml#L) | ansible.builtin.get_url | No | N/A |
| [create cni directories](tasks/binary/setup-cni-plugins.yml#L) | ansible.builtin.file | No | N/A |
| [extract cni plugins](tasks/binary/setup-cni-plugins.yml#L) | ansible.builtin.unarchive | No | N/A |




### File: `tasks/binary/setup-containerd.yml`

| Task Name | Module | Has Conditions | Line |
|-----------|--------|----------------|------|
| [download containerd binary file](tasks/binary/setup-containerd.yml#L) | ansible.builtin.get_url | No | N/A |
| [download containerd verification file](tasks/binary/setup-containerd.yml#L) | ansible.builtin.get_url | No | N/A |
| [extract containerd](tasks/binary/setup-containerd.yml#L) | ansible.builtin.unarchive | No | N/A |




### File: `tasks/binary/set-download-urls.yml`

| Task Name | Module | Has Conditions | Line |
|-----------|--------|----------------|------|
| [set architecture if not defined](tasks/binary/set-download-urls.yml#L) | ansible.builtin.set_fact | No | N/A |
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
| [download runc binary file](tasks/binary/setup-runc.yml#L) | ansible.builtin.get_url | No | N/A |
| [download runc verification file](tasks/binary/setup-runc.yml#L) | ansible.builtin.get_url | No | N/A |
| [install runc binary](tasks/binary/setup-runc.yml#L) | ansible.builtin.copy | No | N/A |




### File: `tasks/binary/main.yml`

| Task Name | Module | Has Conditions | Line |
|-----------|--------|----------------|------|
| [Create Packages Directory](tasks/binary/main.yml#L) | ansible.builtin.file | No | N/A |
| [Set Release Versions](tasks/binary/main.yml#L) | ansible.builtin.import_tasks | No | N/A |
| [Set Download URLs](tasks/binary/main.yml#L) | ansible.builtin.import_tasks | No | N/A |
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
        containerd_binary_link_path: /usr/bin
        containerd_service_binary_path: /opt/containerd/bin

```

## License


license (GPL-2.0-or-later, MIT, etc)


## Author Information


**Author:** gkorkmaz




**GitHub:** [gkorkmaz](https://github.com/gkorkmaz)

---
*This documentation was automatically generated using [docsible](https://github.com/zbohm/docsible).*
<!-- DOCSIBLE END -->
