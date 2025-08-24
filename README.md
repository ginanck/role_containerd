# role_containerd

This Ansible role installs and configures containerd runtime for Kubernetes clusters. It supports both repository-based installation and binary installation methods, automatically configures system parameters, and sets up crictl for container management.

## Features

- Supports multiple installation methods (repository packages or binary downloads)
- Automatically detects and installs latest stable versions from GitHub releases
- Configures systemd cgroup driver for Kubernetes compatibility
- Sets up proper sysctl parameters for container networking
- Installs and configures crictl for container debugging
- Supports both Debian/Ubuntu and RedHat/CentOS distributions
- Handles GitHub API rate limiting with optional access tokens

## Requirements

- Ansible 2.1 or higher
- Target systems running supported Linux distributions (Debian, Ubuntu, RedHat, CentOS)
- Internet connectivity for downloading packages or binaries
- Sudo privileges on target hosts

## Role Variables

### Installation Configuration

| Variable | Default | Description |
|----------|---------|-------------|
| `containerd_setup_type` | `repo` | Installation method: "repo" for package manager or "binary" for direct downloads |

### Binary Paths and Locations

| Variable | Default | Description |
|----------|---------|-------------|
| `containerd_binary_link_path` | `/usr/bin` | Path where containerd binaries are symlinked |
| `containerd_service_binary_path` | `/opt/containerd/bin` | Directory where containerd binaries are installed |
| `containerd_config_file` | `/etc/containerd/config.toml` | Path to containerd configuration file |
| `containerd_systemd_service_file` | `/etc/systemd/system/containerd.service` | Path to containerd systemd service file |

### Version Management

| Variable | Default | Description |
|----------|---------|-------------|
| `containerd_version` | (auto-detected) | Specific containerd version to install |
| `containerd_runc_version` | (auto-detected) | Specific runc version to install |
| `containerd_cni_plugins_version` | (auto-detected) | Specific CNI plugins version to install |
| `containerd_architecture` | `amd64` | Target architecture for binary downloads |

### Container Runtime Configuration

| Variable | Default | Description |
|----------|---------|-------------|
| `containerd_config_systemd_cgroup_enabled` | `true` | Enable systemd cgroup driver for Kubernetes compatibility |
| `containerd_config_disabled_plugins` | `[]` | List of containerd plugins to disable |

### System Configuration

| Variable | Default | Description |
|----------|---------|-------------|
| `containerd_sysctl_conf_file` | `99-containerd.conf` | Sysctl configuration file name |
| `containerd_sysctl_parameters` | See defaults | List of sysctl parameters for container networking |

### CRI Tools Configuration

| Variable | Default | Description |
|----------|---------|-------------|
| `containerd_crictl_runtime_endpoint` | `/run/containerd/containerd.sock` | Runtime endpoint for crictl |
| `containerd_crictl_image_endpoint` | `/run/containerd/containerd.sock` | Image endpoint for crictl |
| `containerd_crictl_timeout` | `10` | Timeout for crictl operations |
| `containerd_crictl_debug` | `false` | Enable debug mode for crictl |
| `containerd_crictl_config_file` | `/etc/crictl.yaml` | Path to crictl configuration file |

## Dependencies

There is no dependencies

## Example Playbook

```yaml
---
- name: Install and configure kubernetes
  hosts: kubernetes
  serial: 1
  become: true
  become_method: sudo
  gather_facts: true
  vars_files:
    - vault/github.yml

  roles:
    - role: role_base
      tags: base
    - role: role_containerd
      tags: containerd
    - role: role_kubeadm
      tags: kubeadm
```

## Configuration

### Ansible Configuration

```ini
[defaults]
host_key_checking = False
inventory = inventory
private_key_file = ~/.ssh/id_rsa
remote_user = ansible
vault_password_file = vault/vault_pass.txt
```

### GitHub Vault Configuration

This role may require GitHub access for downloading components. Create an encrypted vault file at `vault/github.yml`:

```yaml
# vault/github.yml (encrypted with ansible-vault)
github_access_token: <GITHUB-TOKEN>
```

To create and manage the vault file:

```bash
# Create vault password file
echo "your-vault-password" > vault/vault_pass.txt
chmod 600 vault/vault_pass.txt

# Create encrypted vault file
ansible-vault create vault/github.yml

# Or encrypt existing file
ansible-vault encrypt vault/github.yml

# View vault contents
ansible-vault view vault/github.yml

# Edit vault contents
ansible-vault edit vault/github.yml
```

## Usage

### 1. Prepare Inventory

```ini
[kubernetes]
k8s-master-01 ansible_host=192.168.1.10
k8s-worker-01 ansible_host=192.168.1.11
k8s-worker-02 ansible_host=192.168.1.12

[kubernetes:vars]
ansible_user=ansible
ansible_ssh_private_key_file=~/.ssh/id_rsa
```

### 2. Run the Playbook

```bash
ansible-playbook -i inventory site.yml --tags containerd
```

### 3. Verify Installation

```bash
# Check containerd service status
ansible kubernetes -m service -a "name=containerd state=started enabled=yes"

# Verify containerd is running
ansible kubernetes -m shell -a "systemctl is-active containerd"

# Test crictl functionality
ansible kubernetes -m shell -a "crictl version"

# Check container runtime info
ansible kubernetes -m shell -a "crictl info"
```

## License

GPL-2.0-or-later

## Author Information

Gorkem Korkmaz
