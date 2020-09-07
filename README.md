
# Harden Debian distros with Ansible

A repository that leverages public Ansible Galaxy playbooks to help speed up the process of
hardening your Debian/Ubuntu servers.

This playbook is meant to be copied and adjusted as per the individual requirements.

It uses Vagrant to test the implementation, and it's then later used in the `Harden Distros with Packer` repository

## Ansible
### Roles
The list of roles the playbook executes in sequence:
* update-distro
* [jnv.unattended-upgrades][1] (Ansible Galaxy dependency)
* [dev-sec.os-hardening][2] (Ansible Galaxy dependency)
* [dev-sec.ssh-hardening][3] (Ansible Galaxy dependency)
* custom-ssh-user

### Tags
* update-distro
* unattended-upgrades
* os-hardening
* ssh-hardening
* custom-ssh-user

## Usage

### Getting Started
* Copy `custom.yaml.demo` file from the `vars/` directory to `custom.yaml`
* Adjust the variable values in `custom.yaml` to fit your needs.
    * `ssh_server_ports`: The ports you want your ssh server to listen on. Default is `22`
    * `custom_ssh_user_name` Set the username for your new ssh user. *REQUIRED*
    * `custom_ssh_user_public_key` Set the path to your public key. Default is `~/.ssh/id_rsa.pub`

### Sequence of commands
* `vagrant up` -> Start the machine and provision it automatically
* `vagrant --ssh-port=4750 reload` -> Reload the machine once provisioned so the change on `ssh_server_ports` gets acknowledged
* `vagrant --ssh-port=4750 provision` -> Manually provision the machine

[1]: https://github.com/jnv/ansible-role-unattended-upgrades
[2]: https://galaxy.ansible.com/dev-sec/os-hardening
[3]: https://galaxy.ansible.com/dev-sec/ssh-hardening
