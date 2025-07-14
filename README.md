Ansible role init
=========

An Ansible role that sets up a non-root user with passwordless sudo access, designed for post-installation initialization.

This role creates a new user, grants sudo privileges, and configures the system to allow passwordless sudo, enabling secure and consistent privilege escalation for automation.

Common use cases:

- Creating a dedicated Ansible user for automation tasks

- Preparing a clean, minimal user environment before applying infrastructure configurations

- Standardizing privilege escalation settings across hosts

Requirements
------------

Root access (either using the root account or sudo/become).

Role Variables
--------------

- `init_username`: name of the user
- `init_password`: password (for tty access)
- `init_id`: UID/GID of the user
- `init_authorized_keys`: SSH public key(s)

Dependencies
------------

None

Example Playbook
----------------

Run with root after installation:

```yaml
- hosts: all
  vars:
    ansible_user: root
    init_username: your_username
    init_password: your_password
    init_id: 1000
    init_authorized_keys:
      - ssh-rsa XXXXXXXXXX
  vars_prompt:
    - name: ansible_ssh_pass
      prompt: "Root password"
      private: true
  roles:
     - cesargoncalves.init
```

License
-------

GPL-3.0

Author Information
------------------

Role created by [cesargoncalves](https://github.com/cesargoncalves)
