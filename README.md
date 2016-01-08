Flow Manager
============

Installs and configures a GPII Flow Manager instance in cloud-based mode, using the nodejs role.

Most of the work to install the Flow Manager itself is done through passing appropriate defaults to the `ansible-nodejs` role; this role really only does Flow Manager-specific things, as opposed to general "install and configure a nodejs application" tasks that the other role can handle. Specifically:

- the universal `cloudBased.production` config is updated appropriately to the relevant Preferences Server host

- the Flow Manager `cloudBased.development.all.local.json` config is updated appropriately to the relevant Preferences Server host

As of the production configuration at time of writing, the cloud-based Flow Manager does not require URLs for the matchmakers, and they are thus not part of the role.

Requirements
------------

A running preferences server is expected and must be configured in the role variables (see below)

Role Variables
--------------

`flow_manager_preferences_server_host_address`: preferences server host address (default: "preferences.gpii.net")
`flow_manager_environment`: GPII environment; this shouldn't be changed under normal circumstances for this role (Default: "cloudBased.production")

Dependencies
------------

- https://github.com/idi-ops/ansible-facts
- https://github.com/idi-ops/ansible-nodejs

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: flowmanager
      roles:
         - { role: ansible-flow-manager, preferences_server_couchdb_host_address: preferences.gpii.net }

License
-------

MIT.

Author Information
------------------
