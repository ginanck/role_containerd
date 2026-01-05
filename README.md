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



### File: `defaults/main.yml`

| Variable | Default Value | Description |
|----------|---------------|-------------|
| `containerd_setup_type` | `repo` | None |
| `containerd_binary_link_path` | `/usr/bin` | None |
| `containerd_service_binary_path` | `/opt/containerd/bin` | None |
| `containerd_config_file` | `/etc/containerd/config.toml` | None |
| `containerd_config_systemd_cgroup_enabled` | `True` | None |
| `containerd_config_disabled_plugins` | `[]` | None |
| `containerd_systemd_service_file` | `/etc/systemd/system/containerd.service` | None |
| `containerd_sysctl_conf_file` | `99-containerd.conf` | None |
| `containerd_sysctl_parameters` | `[]` | None |
| `containerd_sysctl_parameters.0` | `{}` | None |
| `containerd_sysctl_parameters.0.name` | `net.ipv4.ip_forward` | None |
| `containerd_sysctl_parameters.0.value` | `1` | None |
| `containerd_sysctl_parameters.1` | `{}` | None |
| `containerd_sysctl_parameters.1.name` | `net.ipv6.conf.all.forwarding` | None |
| `containerd_sysctl_parameters.1.value` | `1` | None |
| `containerd_sysctl_parameters.2` | `{}` | None |
| `containerd_sysctl_parameters.2.name` | `vm.swappiness` | None |
| `containerd_sysctl_parameters.2.value` | `0` | None |
| `containerd_crictl_runtime_endpoint` | `/run/containerd/containerd.sock` | None |
| `containerd_crictl_image_endpoint` | `{{ containerd_crictl_runtime_endpoint }}` | None |
| `containerd_crictl_timeout` | `10` | None |
| `containerd_crictl_debug` | `False` | None |
| `containerd_crictl_config_file` | `/etc/crictl.yaml` | None |




## Task Overview


This role performs the following tasks:


### `post-tasks.yml`


- **create containerd config directory**
- **get latest crictl release version without token**
- **get latest crictl release version with token**
- **set crictl_latest from appropriate source**
- **set crictl version from release data**
- **setup crictl binary for repo installation type**
- **create containerd configuration file**
- **create crictl configuration file**
- **install containerd systemd service**
- **restart containerd service**


### `prerequisites.yml`


- **ensure containerd binaries are in PATH**
- **ensure /etc/sysctl.d exists**
- **create sysctl configuration file for containerd**
- **apply sysctl parameters**


### `main.yml`


- **Install Prerequisite Packages**
- **Setup Containerd runtime**
- **Setup Containerd Configuration**


### `binary/setup-cni-plugins.yml`


- **download cni plugins binary file**
- **download cni plugins verification file**
- **create cni directories**
- **extract cni plugins**


### `binary/setup-containerd.yml`


- **download containerd binary file**
- **download containerd verification file**
- **extract containerd**


### `binary/set-download-urls.yml`


- **set architecture if not defined**
- **set download URLs and filenames for each component**


### `binary/set-releases.yml`


- **set default version variables if not defined**
- **get latest releases from GitHub API for binary versions without token**
- **get latest releases from GitHub API for binary versions with token**
- **parse and set versions (use latest stable from GitHub)**
- **set version variables for items with predefined versions**


### `binary/setup-runc.yml`


- **download runc binary file**
- **download runc verification file**
- **install runc binary**


### `binary/main.yml`


- **Create Packages Directory**
- **Set Release Versions**
- **Set Download URLs**
- **Setup Containerd**
- **Setup Runc**
- **Setup CNI Plugins**


### `repo/RedHat.yml`


- **set repository distribution name**
- **install dnf-plugins-core (RedHat family)**
- **download docker repository file (RedHat family)**
- **check if containernetworking-plugins package is available**
- **set packages to install for RedHat**
- **install containerd.io package**


### `repo/Debian.yml`


- **set repository distribution name**
- **install prerequisites (Debian family)**
- **create keyrings directory (Debian family)**
- **check if docker gpg key exists**
- **add docker gpg key (Debian family)**
- **check if docker repository exists**
- **add docker repository (Debian family)**
- **install containerd.io package**


### `repo/crictl.yml`


- **create containerd bin dir**
- **extract crictl**
- **check if versioned crictl binary exists**
- **install crictl to version-specific path**
- **calculate priority from version**
- **set up alternatives for crictl binaries**
- **remove rootless setup scripts**
- **find containerd binary path**
- **set default containerd path**


### `repo/main.yml`


- **Install containerd.io package**




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

## Documentation Maintenance

### Updating Dependencies

1. **Update** `meta/main.yml`:
   ```yaml
   documented_requirements:
     - src: https://github.com/user/role.git
       version: master
     - name: collection.name
       version: 1.0.0
   ```

2. **Sync** `meta/install_requirements.yml` with the same requirements

3. **Regenerate** documentation:
   ```bash
   pre-commit run --all-files
   ```

### Template Updates

- Edit `.docsible_template.md` for structure changes
- Test with: `docsible --role . --md-template .docsible_template.md -nob -com -tl`
- Commit both template and generated README.md

### Quick Checklist

When updating dependencies:
- [ ] Add to `meta/main.yml` → `documented_requirements`
- [ ] Add to `meta/install_requirements.yml`
- [ ] Run `pre-commit run --all-files`
- [ ] Verify generated README.md
- [ ] Commit all changes

## License


license (GPL-2.0-or-later, MIT, etc)


## Author Information


**Author:** gkorkmaz




**GitHub:** [gkorkmaz](https://github.com/gkorkmaz)

---
*This documentation was automatically generated using [docsible](https://github.com/zbohm/docsible).*
<!-- DOCSIBLE END -->
