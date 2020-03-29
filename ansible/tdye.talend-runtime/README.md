# tdye.talend-runtime

Requirements
------------

This role installs a single copy of the Talend Runtime for Talend Cloud on a compute node or VM

A mount point called '/talend_install' is required where the Talend manual install files for the Runtime is stored.

This role is has known to work with Enterprise Talend 7.1.1.

Role Dependencies
-----------------
JDK 1.8 must be preinstalled  
JAVA_HOME must be set before install   


Role Variables
--------------

```yaml
# defaults file for tdye.talend-tac
# talend_root is the installation destination for Talend software
talend_root: /opt/talend-7.1.1
talend_version: 7.1.1

# talend_user and group are the Linux owner and group name of the Talend filesystem
#  these will be created if they do not exist
talend_user: talenduser
talend_group: talendgroup
```

Dependencies
------------
JDK 1.8 must be preinstalled  
JAVA_HOME must be set before install 

Example Playbook
----------------

```yaml
- name: configure and deploy the Talend Runtime software to a node
  hosts: "{{ dynamic_host | default('ec2_tag_name')}}"
  remote_user: root
  become: true
  gather_facts: yes
  environment:
    JAVA_HOME: /usr/java/latest

  roles:
   - tdye.talend-runtime
```

License
-------

Apache License 2.0

Author Information
------------------

This role was created in 2019 by [Thomas A. Dye III, CCP](https://github.com/tdye).

