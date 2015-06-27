Nodejs App [![Build Status](https://travis-ci.org/mtpereira/ansible-nodejs-app.svg)](https://travis-ci.org/mtpereira/ansible-nodejs-app)
=========

Deploys Nodejs applications.

By default, it installs the latest Node version available on [Nodesource's repository](https://deb.nodesource.com/node/) using the [nodesource.node](https://galaxy.ansible.com/list#/roles/1488) role.

Requirements
------------

None.

Role Variables
--------------

Required variables:

* `nodejs_app_repo`: Git repository from where to fetch the app's source. No default.
* `nodejs_app_bin`: Command to be ran by the init script in order to execute the app. No default.
* `nodejs_app_user`: Username for the user that runs the app. Defaults to `nodejs`.
* `nodejs_app_path`: Path for installing the app, which is also the `nodejs_app_user` home. Defaults to `/var/www/nodejs`.
* `nodejs_app_env`: Dictonary with environment variables to feed to the app. Defaults to `[]`.
* `nodejs_app_install_node`: Enables or disables installing nodejs via the `nodesource.node` role. Defaults to `yes`.
* `nodejs_app_force_start`: Force start of the app by the end of the playbook, regardless the presence of changes. Defaults to `no`.
* `nodejs_app_pidfile`: Writes a PID file via the init script. It has no default value and, therefor, does not writes a PID file.

Internal variables, avoid changing:

* `nodejs_app_node_pin_priority`: Pin for `apt-preferences`. Defaults to `500`.

Dependencies
------------

* [nodesource.node](https://galaxy.ansible.com/list#/roles/1488)

These roles can be installed by running `ansible-galaxy install -r requirements.yml`.

Local Testing
-------

Tests can be ran on a Ubuntu Trusty box by executing "vagrant up". There are the following ENV variables:

* `ANSIBLE_TAGS`: A list of tags, comma-separated, that will be ran by Ansible. Defaults to `all`.
* `ANSIBLE_VERBOSE`: Ansible's verbosity level. Defaults to `v`.

Example Playbook
----------------

    - hosts: servers
      roles:
         - role: mtpereira.nodejs-app
           nodejs_app_name: node-js-sample
           nodejs_app_repo: https://github.com/heroku/node-js-sample
           nodejs_app_bin: index.js

License
-------

BSD

Author Information
------------------

Thanks to [nodesource](https://nodesource.com/) for the Nodejs packages repository and Ansible role.

Thanks to [heroku](https://github.com/heroku/) for the sample Nodejs application.

[GitHub project page](https://github.com/mtpereira/ansible-ghost)

[Manuel Tiago Pereira](https://mtpereira.com)
