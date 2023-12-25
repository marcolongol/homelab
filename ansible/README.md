# 🤖 Ansible

This directory contains one playbook for each of the wrapper roles below, each wrapper role is a collection of roles with some additional tasks that are used to configure the host server os VM(s) with a specific purpose. The `site.yml` file is the main playbook that triggers the installation and configuration of the whole infrastructure.

- `common`: Installs common packages and applies common configurations. Wraps the following roles:
  - `singleplatform-eng.users`: Creates users and groups.
  - `dev-sec.ssh-hardening`: Hardens the SSH configuration.
  - `Oefenweb.apt`: Updates the apt cache and upgrades the system.
  - `geerlingguy.ntp`: Installs and configures NTP.
  - `Oefenweb.fail2ban`: Installs and configures fail2ban.
- `proxmox`: Installs Proxmox VE 7.4-17 on the host server, configures networking, storage and provisions the VMs using cloud-init images. Wraps the following roles:
  - `lae.proxmox`: Installs Proxmox VE and configures proxmox.
- `docker`: Installs Docker on the docker and configures it with the necessary settings, also manages deployment of applications. Wraps the following roles:
  - `geerlingguy.docker`: Installs Docker.

## 📁 Directory Structure

```bash
./ansible
├── collections/ # Folder containing the ansible collections
├── group_vars/ # Folder containing the group variables
├── playbooks/ # Folder containing the playbooks
├── roles/ # Folder containing the roles
│   ├── common/ # Folder containing the common role
│   ├── docker/ # Folder containing the docker role
│   ├── proxmox/ # Folder containing the proxmox role
├── site.yml # Main playbook
├── inventory.yml # Inventory file
├── ansible.cfg # Ansible configuration
├── requirements.yml # Ansible requirements
└── README.md # Ansible README
```

## 🚀 Usage

1. Set `ANSIBLE_CONFIG` environment variable to the `ansible.cfg` file:

   ```bash
   export ANSIBLE_CONFIG=./ansible.cfg
   ```

2. Install Ansible and the required collections/roles:

   ```bash
   pip install ansible
   ansible-galaxy collection install -r requirements.yml
   ```

3. Update the `inventory.yml` file.

4. Customize the `group_vars` files.

5. Run the `site.yml` playbook:

   ```bash
   ansible-playbook site.yml
   ```
