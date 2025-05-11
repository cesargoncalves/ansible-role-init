Ansible role init
=========

Ansible role that creates a new user, grants it sudo privileges, and configures sudoers to allow passwordless sudo access. This role is intended to be used after installation. The purpose is to establish a non-root user with the necessary permissions to run subsequent playbooks.

Typical use cases include:

- Creating a dedicated Ansible user for automation tasks

- Preparing a clean user environment before running infrastructure configuration

- Ensuring consistent privilege escalation settings across hosts

Requirements
------------

None

Role Variables
--------------

- `init_username`: name of the user
- `init_password`: password of the user (for tty access)
- `init_uid`: UID/GID of the user
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
    init_uid: 1000
    init_authorized_keys:
      - ssh-rsa XXXXXXXXXX
  vars_prompt:
    - name: ansible_ssh_pass
      prompt: "SSH password"
      private: true
  roles:
     - cesargoncalves.init 
```

Subsequent exections:

```yaml
- hosts: all
  become: true
  vars:
    ansible_user: your_username
  roles:
     - cesargoncalves.init 
```

License
-------

GPL-3.0

Author Information
------------------

Role created by [cesargoncalves](https://github.com/cesargoncalves)
