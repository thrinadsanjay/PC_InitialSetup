# Ansible System Setup and VM Provisioning Role

This project provides an Ansible role and associated playbooks to automate the initial setup of a Linux system, including disk partitioning, LVM setup, network bridge configuration, and installation of virtualization tools. It also supports automated deployment of virtual machines using ISO images.

## 📁 Project Structure

init_setup/
├── defaults/
│   └── main.yml
├── files/
├── handlers/
│   └── main.yml
├── meta/
│   └── main.yml
├── tasks/
│   └── main.yml
├── templates/
├── vars/
│   └── main.yml
├── README.md


## 🚀 Features

- Detects and uses available free disk space for partitioning
- Automatically creates LVM volumes and mounts them
- Installs essential virtualization packages (`libvirt`, `cockpit`, etc.)
- Sets up a bridged network interface using the first available Ethernet connection
- Starts and enables `libvirtd` and `cockpit` services
- Supports VM deployment using ISO and automated installation config

## ✅ Requirements

- Ansible 2.10+
- Linux host (tested on RHEL-like systems)
- `community.general` collection:


## 🔧 Role Variables

You can configure these variables in the playbook or `defaults/main.yml`:

```yaml
device: <device name (/dev/sda)>

partitions_required:
- label: <Mount point label>
  size_gb: <Desired Size>
  vg: <Volume Group name>
  lv: <Logical Volume Name>
  mount_point: <Mount Point>

bridge_name: <bridge interface name>
admin_user: <user name>

required_packages:
- <List of Required Packages>

IP_address: <IP Address>
NetMask: <Netmask>

## 📦 Usage


Create below Playbook in desired Location

main.yml
---------------------------------------------
|  ---                                      |
|  - name: Perform Initial Setup of PC.     |
|    hosts: <host>                          |   
|    become: true                           |
|    roles:                                 |
|      - init_setup                         |
---------------------------------------------

Run Below command to execute the playbook

# ansible-playbook main.yml

## 🧠 Notes
The role is idempotent and skips existing partitions/mounts.

Automatically detects standard Ethernet interfaces (ethernet, 802-3-ethernet).

Bridge configuration avoids using wireless interfaces.

## 👨‍💻 Contributing
Feel free to fork and contribute via pull requests! Feedback and enhancements welcome.

## 📄 License
MIT License

Let me know if you'd like to include example playbook snippets or add Galaxy publishing instructions.
