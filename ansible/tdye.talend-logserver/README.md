# tdye.talend-logserver

Requirements
------------

This role installs the Talend Logserver components on a compute node or VM

A mount point called '/talend_install' is required where the Talend manual install files for logserver is stored.

This role is has known to work with Enterprise Talend 7.2.

Role Dependencies
-----------------
williamyeh.oracle-java

Role Variables
--------------

```yaml
talend_root: /opt/talend-7.0.1
talend_version: 7.0.1

talend_user: talend
talend_group: talend


# Logserver params
talend_logserver_install_path: /talend_install/Manual_Installation/logserver
talend_logserver_zip: Talend-LogServer-V7.0.1-linux-x86_64.tar.gz


# Azure FS parameters
azure_vm: true	
az_username: XXXXXXXXXXX
az_password: YYYYYYYYYYYYYYYYYYYYY
az_src: //ZZZZZZZZZZZZZZZZ.file.core.windows.net/<share name>
az_path: /talend_install

```

Dependencies
------------


Example Playbook
----------------

```yaml
- name: configure and deploy the TAC software to a node
  hosts: "{{ dynamic_host | default('ec2_tag_name')}}"
  remote_user: root
  become: true
  gather_facts: yes

  roles:
   - tdye.talend-logserver
```

License
-------

Apache License 2.0

Author Information
------------------

This role was created in 2018 by [Thomas A. Dye III, CCP](https://github.com/tdye).

