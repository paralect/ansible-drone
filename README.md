Ansible Drone
=========

An ansible role for the [drone](https://github.com/drone/drone) CI deployment with Github integration and PostgreSQL database.

Requirements
------------

[Docker](https://www.docker.com/) must be installed on the server in order to use this role. If you don't have docker on your server we recommend [angstwad.docker_ubuntu](https://github.com/angstwad/docker.ubuntu) Ansible role.

Role Variables
--------------

Available variables:

```
# Version of Drone CI, see other versions here: https://hub.docker.com/r/drone/drone/tags/
drone_version: latest

# List of users with admin access to the drone, readme more: http://docs.drone.io/user-management/
drone_admins: ""

# Name of the docker agent container, you can add more than one agent
drone_agents: [{name: "Nancy"}]

# the url, where drone instance will be publicly available
# typically you would have nginx in front of Drone CI
drone_host:

# Drone secret key, used for private communication between agent and web UI
# more info: http://docs.drone.io/install-for-github/
drone_secret: hTirsXmrY4YsyK79ELgB

# Github oauth application client identifier, more info http://docs.drone.io/install-for-github/
drone_github_client:
# Github oauth application client secret, more info http://docs.drone.io/install-for-github/
drone_github_secret:

# A password to postress db used by drone
drone_postgress_password: droneRocks23@p
# A username to postress db used by drone, read more: http://docs.drone.io/database-settings/
drone_postgress_user: drone
# A name of to postress db used by drone, read more: http://docs.drone.io/database-settings/
drone_postgress_db: drone
# a directory on a host machine, where postresql data stored
drone_postress_data_dir: /drone-postgres-data

# Internal drone ui http url used by nginx to proxy traffic. For example: http://localhost:8000
nginx_drone_internal_host: http://localhost:8000

```

Dependencies
------------

[Docker](https://www.docker.com/) must be installed on the server in order to use this role. If you don't have docker on your server we recommend [angstwad.docker_ubuntu](https://github.com/angstwad/docker.ubuntu) Ansible role.

Example Playbook
----------------

```
---
- name: Deploy drone CI server
  hosts: drone
  become_user: root
  become: true
  roles:
    - role: paralect.drone
      # Version of Drone CI, see other versions here: https://hub.docker.com/r/drone/drone/tags/
      drone_version: latest

      # the url, where drone instance will be publicly available
      # typically you would have nginx in front of Drone CI
      drone_host: http://178.62.116.103

      # Drone secret key, used for private communication between agent and web UI
      # more info: http://docs.drone.io/install-for-github/
      drone_secret: hTirsXmrY4YsyK79ELgB

      # Github oauth application client identifier and secret, more info http://docs.drone.io/install-for-github/
      drone_github_client:
      drone_github_secret:

      # A password to postress db used by drone
      drone_postgress_password: droneRocks23@p
      # A username to postress db used by drone, read more: http://docs.drone.io/database-settings/
      drone_postgress_user: drone
      # A name of to postress db used by drone, read more: http://docs.drone.io/database-settings/
      drone_postgress_db: drone
      # a directory on a host machine, where postresql data stored
      drone_postress_data_dir: /drone-postgres-data
```

License
-------

MIT
