# tdye.talend-rjs

Requirements
------------

This role installs the Talend Remote Job server on a compute node or VM

A mount point called '/talend_install' is required where the Talend manual install files for TAC is stored.

This role is has known to work with Enterprise Talend 6.5 and 7.0.

Role Dependencies
-----------------
JDK 1.8 must be preinstalled

Role Variables
--------------

```yaml
# defaults file for tdye.talend-tac
# talend_root is the installation destination for TAC
talend_root: /opt/talend-7.0.1
talend_version: 7.0.1

# talend_user and group are the Linux owner and group name of the TAC filesystem
talend_user: talenduser
talend_group: talendgroup


# RJS params
# talend_rjs_zip is the RJS manual installer file downloaded from Talend
talend_rjs_zip: Talend-JobServer-XXXXXXX-V7.0.1.zip

talend_rjs_nstall_path: /talend_install/Manual_Installation/RJS

```

Dependencies
------------
JDK 1.8 must be preinstalled

Example Playbook
----------------

```yaml
- name: configure and deploy the TAC software to a node
  hosts: "{{ dynamic_host | default('ec2_tag_name')}}"
  remote_user: root
  become: true
  gather_facts: yes

  roles:
   - tdye.talend-rjs
```

License
-------

Apache License 2.0

Author Information
------------------

This role was created in 2018 by [Thomas A. Dye III, CCP](https://github.com/tdye).

