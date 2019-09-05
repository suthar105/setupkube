Role Name
=========

A brief description of the role goes here.

Requirements
------------

This role requires fresh installation of CentOS in 3 machines. 1 for Kubemaster and 2 servers for Kubenodes. As we are going to run Ansible playbooks on all 3 servers so python packages should be installed already. Apart from that, key based authentication should be configured on all 3 servers, so that ansible-controller node can communicate and run playbook on them. The Ansible will run playbook as "root" user, so make sure that key based authentication is setup for root user.

Setup Key based authentication:
Generate SSH keys in your local first:
ssh-keygen -t rsa

This will generate $HOME/.ssh/id_rsa and $HOME/.ssh/id_rsa.pub files. Now you need to copy public key(id_rsa.pub) from your local to all 3 remote nodes.

For copying public key from local to all 3 remote servers, run below command.

ssh-copy-id root@<kubemaster_ip>

This will ask you for password, so enter password.

Update Inventory file before running this role.

inventory.txt
all: # keys must be unique, i.e. only one 'hosts' per group
    hosts:
        kubemaster:
            ansible_host: 192.168.10.223
            ansible_user: root
        kubenode1:
            ansible_host: 192.168.10.83
            ansible_user: root
        kubenode2:
            ansible_host: 192.168.10.206
            ansible_user: root

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
