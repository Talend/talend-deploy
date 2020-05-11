# talend-deploy
Ansible scripts for deploying traditional Talend infrastructure such as TAC, Job Server, Nexus, LogServer, Filebeat.

Pre-requisites
------------

1) Ansible

2) Python3 must be installed on the controller node


AWS dynamic inventory
------------

These scripts can also dynamically deploy the Talend infrastructure on the EC2 servers based on their EC2 tag names.


1) Place ec2.py & ec2.ini in `/etc/ansible` directory

2) Export environment variables to configure ec2 dynamic inventory

````bash
export ANSIBLE_INVENTORY=/etc/ansible/ec2.py
export AWS_ACCESS_KEY_ID=<your_aws_access_key_id>
export AWS_SECRET_ACCESS_KEY=<your_aws_secret_access_key>
````

Role Dependencies and Requirements
-----------------

All role level dependecies and requirements can be found under each role's individual README.md file.
Example: For TAC role, one can find the dependecies and requirements at `talend-deploy/roles/tdye.talend-tac/README.md`


Example Playbook
----------------

````yaml
---
- name: Install TAC
  hosts: td_tac_group
  become: yes
  become_user: root
  become_method: sudo
  remote_user: centos
  gather_facts: yes
  vars_files:
    - vars/talend.yml
  roles:
    - java
    - tdye.talend-common
    - utils
    - tdye.talend-tac
  tags:
    - tac
````

Example Playbook Run Command
----------------

Use example playbook with static hosts files

````bash
ansible-playbook -i example/inventory tac.yml   --extra-vars "dynamic_host=tag_Name_EC2_TAG_NAME"
````

Use AWS dynamic inventory

````bash
ansible-playbook -i example/inventory tac.yml   --extra-vars "dynamic_host=tag_Name_EC2_TAG_NAME"
````


License
-------

Apache License 2.0

Author Information
------------------

Created in 2018 by [Thomas A. Dye III, CCP](https://github.com/tdye).

