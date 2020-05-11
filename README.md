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

Getting Started
----------------

1.  clone git repo
2.  switch to development branch if desired
3.  download license file and place in root directory of cloned repo
4.  change talend license userid and password in vars/talend.yml
5.  update database connectivity in vars/talend.yml
6.  retrieve jdbc driver and load it to location specified in vars/talend.yml tac_db_jdbc_driver
7.  modify example/inventory
8.  modify example/group_vars/all if desired, but defaults shoudl be ok
9.  run a playbook


Example Playbook Run Command
----------------

Use example playbook with static hosts files

````bash
ansible-playbook -i example/inventory tac.yml 2>&1 | tee tac.log
````

Use AWS dynamic inventory

````bash
ansible-playbook -i example/inventory tac.yml --extra-vars "dynamic_host=tag_Name_EC2_TAG_NAME" 2>&1 tac.log
````



License
-------

Apache License 2.0

Author Information
------------------

Created in 2018 by [Thomas A. Dye III, CCP](https://github.com/tdye).

