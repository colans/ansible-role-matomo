Consensus Enterprises' Matomo
=============================

Consensus Enterprises' Ansible role for provisioning Matomo (formerly known as "Piwik").

Overview
--------

This role does the following:

1. Adds an Nginx site configuration.
1. Gets an HTTPS certificate (if HTTPS support is enabled).
1. Adds a configuration file for the application.
1. Creates and populates the application's database.
1. Installs the Debian package, automatically updating the database if the template is too old.
1. Installs the recommended GeoIP data file, which can be enabled in the application's settings.

Requirements
------------

* A Debian-based OS (e.g. Ubuntu)
* The Nginx Web server
* MySQL (version 5.5 or greater) or MariaDB
* A DNS record pointing to the instance (e.g. `matomo.example.com`)

We'd be happy to include support for other operating systems, Web servers or anything else.  Patches welcome!

Role Variables
--------------

See [defaults/main.yml](https://gitlab.com/consensus.enterprises/ansible-roles/ansible-role-matomo/blob/master/defaults/main.yml) for all role variables.

Dependencies
------------

### geerlingguy.certbot

[geerlingguy/certbot](https://galaxy.ansible.com/geerlingguy/certbot) is used for the HTTPS certificate management, installation and renewals.

See the [default variables used](https://gitlab.com/consensus.enterprises/ansible-roles/ansible-role-matomo/blob/master/tasks/get-https-certificate.yml) when calling it.

Example Playbook
----------------

```yaml
- hosts: servers
  become: true
  roles:
    - ansible-role-matomo
  vars:
    # https://github.com/ansible/ansible/issues/45852
    # https://www.toptechskills.com/ansible-tutorials-courses/how-to-fix-usr-bin-python-not-found-error-tutorial/
    ansible_python_interpreter: /usr/bin/python3
    # Main role variable settings.
    matomo_domain: matomo.example.com
    matomo_https_certificate_admin_email: tech@example.com
    matomo_superuser_password: YOUR_SUPER_SECRET_ADMIN_PASSWORD_FOR_THE_WEB_UI
```

Testing
-------

Tests can be run like so (with more or fewer "v"s for verbosity):

```sh
ansible-playbook -vv --ask-become-pass --inventory TARGET_HOSTNAME, /path/to/this/role/tests/TEST_NAME.yml
```

Feel free to add your own tests in `tests/`, using existing ones as examples.  Contributions welcome.

Issue Tracking
--------------

For bugs, feature requests, etc., please visit the [issue tracker](https://gitlab.com/consensus.enterprises/ansible-roles/ansible-role-matomo/-/boards).

License
-------

GNU AGPLv3

Author Information
------------------

Written by [Colan Schwartz](https://consensus.enterprises/team/colan/) and other folks at [Consensus Enterprises](https://consensus.enterprises/).  To contact us, please use our [Web contact form](https://consensus.enterprises/#contact).
