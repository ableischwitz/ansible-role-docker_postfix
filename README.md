Role Name
=========

This role handles the deployment and start of a dockerized postfix instance.

Requirements
------------

Any pre-requisites that may not be covered by Ansible itself or the role should be mentioned here. For instance, if the role uses the EC2 module, it may be a good idea to mention in this section that the boto package is required.

Role Variables
--------------

# provide network for inter-container messaging
postfix_docker_network: isolated_nw

# define storage-path for persistent storage, used for spool, logs and configuration-scripts
postfix_persistent_storage: "{{ global_persistend_storage }}/postfix"

# define mail-name. This should be FQDN
postfix_mailname: smtp.example.com

# Postfix base-configuration, even more details can be applied by using the template-files.
# ToDo: fix detection of docker-network
# Don't know if that is usable prior start of a container, but that is returned - somewhat.
# {{ postfix_docker_network }}.<whatever_stands_for_network>/{{ postfix_docker_network }}.IPPrefixLen
postfix_my_networks: "{{ ansible_docker0.ipv4.network }}/24 127.0.0.8/8"
postfix_my_destination: "localhost.localdomain, localhost, example.com"
postfix_root_alias: root@otherhost

Dependencies
------------

A list of other roles hosted on Galaxy should go here, plus any details in regards to parameters that may need to be set for other roles, or variables that are used from other roles.

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: servers
      roles:
         - { role: ansible-role-docker_postfix, tags: ['postfix'] }

License
-------

GPLv3

Author Information
------------------

