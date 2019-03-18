Ubuntu Base
=========

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

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: all
      roles:
         - { role: vermilion-tech.ubuntu-base }

License
-------

BSD

Author Information
------------------

Kaden Nelson
`kaden@vermilion.tech`
vermilion.tech
