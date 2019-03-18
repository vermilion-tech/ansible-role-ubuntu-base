Ubuntu Base
=========
https://galaxy.ansible.com/kadenlnelson/ansible_role_ubuntu_base

Installs, Updates, and Upgrades packages using `apt`. Installs `docker` and `python-pip` using `geerlingguy` roles. Installed packages can be modified using variables. See `Role Variables`.

Requirements
------------

Requires Python

Role Variables
--------------

`apt.upgrade` defaults to `dist`
`apt.autoclean && apt.autoremove` defaults to `yes`

`apt.install_packages` installs `htop` by default

Dependencies
------------

See `vars/main.yml` for configurable options
- geerlingguy.docker
- geerlingguy.pip
  - installs `docker` and `docker-compose by default`

Example Playbook
----------------
`$ ansible-galaxy install kadenlnelson.ansible_role_ubuntu_base`

    - hosts: all
      roles:
         - { role: kadenlnelson.ansible_role_ubuntu_base }

License
-------

BSD

Author Information
------------------

Kaden Nelson
`kaden@vermilion.tech`
vermilion.tech
