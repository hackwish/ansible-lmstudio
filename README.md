LM Studio Installer role
=========

This role install LmStudio for Linux Debian based and Mac Silicon/arm based systems *(because the install package supports that)*.

Requirements
------------

- Linux Debian based system
- MacOS Silicon ARM based system
- Ansible

Role Variables
--------------

defaults (current):
- appName: LM-Studio
- version: 0.4.20
- build: 1

Dependencies
------------

NaN

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: servers
      roles:
         - { role: username.rolename, x: 42 }

License
-------

BSD

Author Information
------------------

Build ByDefault.

Test
----

``ansible-playbook tests/test.yml -i tests/inventory --syntax-check``
