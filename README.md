Barman
=========

Install and configure barman
Inspired from alexey-medvedchikov.barman

Requirements
------------

For SSH mode with rsync (default) :
You should configure your pg server to send wal logs through rsync. Example, in pg server configuration file :

    wal_level = 'archive'
    archive_mode = on
    archive_command = 'rsync -ap --bwlimit=1000 %p {{barman_user}}@{{this host}}:{{barman_home}}/{{name}}/%f'

For streaming replication mode :
Working with Postgresql >= 9.4 and barman >= 2.0
You should configure replication slots in your pg servers so that barman can connect to it

    wal_level = 'logical'
    max_wal_senders should be > 0
    max_replication_slots should be > 0

This playbook can create automatically the slot with the command

    barman receive-wal --create-slot <server host>


You should create the replication slot yourself with psql function pg_create_physical_replication_slot or use the command line

    pg_recvlogical -S {{barman_slot_name}} --create
 


Role Variables
--------------

A description of the settable variables for this role should go here, including any variables that are in defaults/main.yml, vars/main.yml, and any variables that can/should be set via parameters to the role. Any variables that are read from other roles and/or the global scope (ie. hostvars, group vars, etc.) should be mentioned here as well.

Dependencies
------------

A list of other roles hosted on Galaxy should go here, plus any details in regards to parameters that may need to be set for other roles, or variables that are used from other roles.

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

An optional section for the role authors to include contact information, or a website (HTML is not allowed).
