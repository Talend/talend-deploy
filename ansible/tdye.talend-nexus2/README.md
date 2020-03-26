# tdye.talend-nexus

Requirements
------------

This role will install the Talend Artifact Repository (Nexus 2) and is intended to be a companion role to the tdye.talend-tac and/or the 
tdye.talend-ci role.  

As Nexus 2 is no longer available from Talend, the software must be downloaded from the sonatype website.  

This role will create the basic Talend repos, but not the security roles and users (at this time).


Role Dependencies
-----------------

A suitable Oracle JVM must be preinstalled before this role is called.

Role Variables
--------------

```yaml
talend_root: /opt/talend-7.0.1
talend_version: 7.0.1

talend_user: talend
talend_group: talend


# Nexus params
talend_install_path: /talend_install/Manual_Installation/TAC
nexus_archive: nexus-2.14.9-01-bundle.tar.gz
nexus_bin: nexus-2.14.9-01/bin

nexus_port: 8081                    # Default is 8081
nexus_user: admin					# Required to create 'thirdparty' repo
nexus_password: Talend123			# Required to create 'thirdparty' repo


### Azure FS parameters
azure_vm: false

# install source mount
az_username: XXXXXXXXXXXXX
az_password: YYYYYYYYYYYYYYYYYYYYYYYYYYYYYYYYYYYYYYYYYYYYYYYY
az_src: //ZZZZZZZZZZZZZZZZZZZ.file.core.windows.net/QQQQQQQQQQQQQQQQQ
az_path: /talend_install

```

Dependencies
------------
JVM 1.8


Example Playbook
----------------

```yaml
- name: configure and deploy the TAC software to a node
  hosts: all
  remote_user: root
  become: true
  gather_facts: yes

  roles:
   - tdye.talend-nexus
```

License
-------

Apache License 2.0

Author Information
------------------

This role was created in 2018 by [Thomas A. Dye III, CCP](https://github.com/tdye).

