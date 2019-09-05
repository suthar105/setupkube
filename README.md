Role Name
=========

A brief description of the role goes here.

Requirements
------------

This role requires fresh installation of CentOS in 3 machines. 1 for Kubemaster and 2 servers for Kubenodes. As we are going to run Ansible playbooks on all 3 servers so python packages should be installed already. Apart from that, key based authentication should be configured on all 3 servers, so that ansible-controller node can communicate and run playbook on them. The Ansible will run playbook as "root" user, so make sure that key based authentication is setup for root user.

Setup Key based authentication:
Generate SSH keys in your local first:
<pre>
ssh-keygen -t rsa
</pre>
This will generate $HOME/.ssh/id_rsa and $HOME/.ssh/id_rsa.pub files. Now you need to copy public key(id_rsa.pub) from your local to all 3 remote nodes.

For copying public key from local to all 3 remote servers, run below command.
<pre>
ssh-copy-id root@<kubemaster_ip>
</pre>
This will ask you for password, so enter password.

Update Inventory file before running this role.

inventory.txt
<pre>
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
</pre>
Role Variables
--------------

The variabls are defined in vars/main.yaml file. 
- kube_token: This is the hardcode token which will be used while setting up kubernetes cluster and joining kube cluster. You can change it to any value but keep the format as is.
- pod_network_cidr: In this role, I have used flunnel as CNI. If you have any other choice, then you can change CIDR value as per your need. 
- kubeuser: This variable will have the username by which you will be interacting with the kubernetes cluster. In this role, I have wrote code to setup user which will have limited priviledges but still it can interact with kubernetes cluster. 

Dependencies
------------

A list of other roles hosted on Galaxy should go here, plus any details in regards to parameters that may need to be set for other roles, or variables that are used from other roles.

Example Playbook
----------------

To use this role, first you need to download entire role from Github or from Ansible Galaxy.
<pre>   
ansible-galaxy install alpeshbhavsar.setupkube
</pre>
Use Role as shown below.
<pre>
---
- hosts: all
  become: yes
  roles:
    - role: alpeshbhavsar.setupkube
</pre>

License
-------

MIT

Author Information
------------------

An optional section for the role authors to include contact information, or a website (HTML is not allowed).
