

### **README.md**
Automated KVM Virtual Machine Provisioning Using Ansible.


```markdown
# Provision-Kvm-Ansible

**Automated KVM Virtual Machine Provisioning Using Ansible**

This project leverages **Ansible** to automate the deployment and management of **KVM virtual machines** on Ubuntu and CentOS hosts. It streamlines the installation of KVM, prepares base QCOW2 images, and provisions new virtual machines with pre-configured networking and SSH access.

---

## Features

- Install and configure KVM, Libvirt, and required virtualization tools on Ubuntu and CentOS hosts.
- Download and prepare base cloud QCOW2 images for VM creation.
- Automate VM provisioning with:
  - Disk creation and cloning from base image.
  - Hostname configuration.
  - SSH key injection for secure access.
  - Network configuration via Netplan.
  - VM creation and startup using `virt-install`.
- Modular Ansible playbooks for reusability and easy customization.

---

## Project Structure

```

Provision-Kvm-Ansible/
│
├─ create_vm.yml          # Playbook to provision a new VM from a base image
├─ prepare_image.yml      # Playbook to download and prepare the base QCOW2 image
├─ provision_host.yml     # Playbook to install KVM and configure the host
├─ inventory              # Ansible inventory file defining target hosts
└─ vars/
└─ vm_settings.yml    # Variable definitions (VM specs, image paths, SSH keys)

````

---

## Prerequisites

- Ubuntu or CentOS target host(s)
- Ansible installed on the control machine
- Internet connectivity on target hosts to download the base image
- Sudo or root access on target hosts

---

## Usage

### 1. Provision KVM Host

Run the playbook to install KVM and required tools:

```bash
ansible-playbook -i inventory provision_host.yml
````

---

### 2. Prepare Base VM Image

Download and prepare the base cloud image:

```bash
ansible-playbook -i inventory prepare_image.yml
```

---

### 3. Create and Provision a New VM

Provision a new VM with customized hostname, SSH access, and network configuration:

```bash
ansible-playbook -i inventory create_vm.yml
```

---

## Configuration

Edit `vars/vm_settings.yml` to define VM parameters such as:

```yaml
vm_name: "my-vm"
vm_memory_mb: 2048
vm_cpus: 2
vm_bridge: "br0"
vm_os_variant: "ubuntu22.04"
base_image_path: "/var/lib/libvirt/images/ubuntu-base.qcow2"
local_ssh_public_key_file: "~/.ssh/id_rsa.pub"
remote_key_dest: "/tmp/id_rsa.pub"
```

---

## Dependencies

* Ansible 2.9+
* KVM / QEMU
* libvirt / virt-manager
* virt-customize and virt-install
* libguestfs-tools


---

## Author

**Mazin Khaled**
DevOps / Virtualization Enthusiast
