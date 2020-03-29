# talend-deploy
Ansible scripts for deploying traditional Talend infrastructure such as TAC, Job Server, Nexus, LogServer, Filebeat. These scripts dynamically deploy the Talend infrastructure on the given EC2 servers based on their EC2 tag names.

Requirements to setup Ansible environment
------------
1) Ansible & Python3 must be installed on the Ansible server

2) One needs to place ec2.py & ec2.ini in /etc/ansible directory

3) One needs to export some environment variables in order to get the ec2 tag name dynamically from AWS

```yaml
export ANSIBLE_INVENTORY=/etc/ansible/ec2.py
export AWS_ACCESS_KEY_ID=<your_aws_access_key_id>
export AWS_SECRET_ACCESS_KEY=<your_aws_secret_access_key>
```

Role Dependencies and Requirements
-----------------

All role level dependecies and requirements can be found under each role's individual README.md file.
Example: For TAC role, one can find the dependecies and requirements at talend-deploy/ansible/tdye.talend-tac/README.md


Example Playbook
----------------

```yaml
- name: configure and deploy the TAC software to a node
  hosts: "{{ dynamic_host | default('ec2_tag_name')}}"
  remote_user: root
  become: true
  gather_facts: yes

  roles:
   - tdye.talend-tac
```

Example Playbook Run Command
----------------
```yaml
ansible-playbook  ~/Ansible/tac.yml   --extra-vars "dynamic_host=tag_Name_EC2_TAG_NAME"
```

License
-------

Apache License 2.0

Author Information
------------------

Created in 2018 by [Thomas A. Dye III, CCP](https://github.com/tdye).

