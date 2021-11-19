
# Harden Debian distros with Ansible

A repository that leverages public Ansible Galaxy playbooks to help speed up the process of
hardening your Debian/Ubuntu servers.

This playbook is meant to be copied and adjusted as per the individual requirements, serving as the
foundation of further refinement of your servers.

*Vagrant* is used to test the logic.

## Ansible
### Roles
The list of roles the playbook executes in sequence:
* [apt](./roles/apt/)
* [custom-ssh-user](./roles/custom-ssh-user)
* [jnv.unattended-upgrades][1] (external dependency) - Check out their page to see the list of supported variables.
* [dev-sec.os-hardening][2] (external dependency) - Check out their page to see the list of supported variables.
* [dev-sec.ssh-hardening][3] (external dependency) - Check out their page to see the list of supported variables.
* [oefenweb.fail2ban][4] (external dependency)
* [oefenweb.ufw][5] (external dependency)

### Role ags
* apt
* custom-ssh-user
* unattended-upgrades
* os-hardening
* ssh-hardening
* fail2ban
* ufw

## Usage

### Variables
* defaults/main.yaml

### Getting Started
* Copy `custom.yaml.demo` file from the `vars/` directory to `custom.yaml`
* Adjust the variable values in `custom.yaml` and `configs. to fit your needs.
    * `custom_ssh_user_name` Set the username for your new ssh user. *REQUIRED*
    * `custom_ssh_user_public_key` Set the path to your public key. Default is `~/.ssh/id_rsa.pub`
    * `custom_ssh_main_server_port`: The ports you want your ssh server to listen on. Default is `22`

### Sequence of commands
* `vagrant up` -> Start the machine and provision it automatically
* `vagrant --ssh-port=4750 reload` -> Reload the machine once provisioned so the change on `ssh_server_ports` gets acknowledged
* `vagrant --ssh-port=4750 provision` -> Manually provision the machine

[1]: https://github.com/jnv/ansible-role-unattended-upgrades
[2]: https://galaxy.ansible.com/dev-sec/os-hardening
[3]: https://galaxy.ansible.com/dev-sec/ssh-hardening
[4]: https://galaxy.ansible.com/oefenweb/fail2ban
[5]: https://galaxy.ansible.com/oefenweb/ufw
