Etherpad
============

Installs and configures a Etherpad instance, using the nodejs role.

Most of the work to install the Etherpad itself is done through passing appropriate defaults to the `ansible-nodejs` role; this role completes the installation of Etherpad done by ansible-nodejs role.

- Installs addtional local npm packages
- Configures the file settings.json

Requirements
------------

- The application is self-contained as it use a sqlite database at the moment.

Role Variables
--------------

- `etherpad_title`: Name of the Etherpad instance (Default: "Etherpad")
- `etherpad_npm_packages`: List of npm packages to install locally, the plugins may be listed here.
- `etherpad_admin_password`: Admin password, if is set it allows the user authentication. If it's empty the two following variables will be ignored.
- `etherpad_admin_users`: Dictionary with username: password to be admins {admin1: admin1pw, admin2: admin2pw}
- `etherpad_users`: Dictionary with username: paswword to be plain users {user1: user1pw, user2: user2pw, user3: user3pw}

Dependencies
------------

- https://github.com/idi-ops/ansible-facts
- https://github.com/idi-ops/ansible-nodejs

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    ---
    
    - hosts: all
      sudo: true
    
      vars:
        nodejs_app_name: etherpad
        nodejs_app_install_dir: /opt/{{ nodejs_app_name }}
        nodejs_app_git_repo: https://github.com/ether/etherpad-lite.git
        nodejs_app_git_branch: 1.5.7
        nodejs_app_commands:
          - "bin/installDeps.sh"
        nodejs_app_start_script: "node_modules/ep_etherpad-lite/node/server.js"
        nodejs_app_host_address: 127.0.0.1
        nodejs_app_tcp_port: 9001
        nodejs_app_test_http_endpoint: /
        nodejs_app_test_http_status_code: 200
        nodejs_app_test_string: "<button type=\"submit\">OK</button>"
        
        etherpad_title: "IDI Etherpad"
        etherpad_npm_packages:
          - sqlite3
        
        etherpad_admin_password: password
        etherpad_admin_users: {admin1: admin1pw, admin2: admin2pw}
        etherpad_users: {user1: user1pw, user2: user2pw, user3: user3pw}
        
      roles:
        - ansible-facts
        - ansible-nodejs
        - ansible-etherpad

License
-------

MIT.

Author Information
------------------
