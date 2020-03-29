# tdye.talend-nexus

Requirements
------------

This role will install the Talend Artifact Repository (Nexus 3) and is intended to be a companion role to the tdye.talend-tac role.  
Nexus is bundled with the TAC installer, and the TAC manual installer must be present for this role to work.

The tdye.talend-tac role can optionally download the TAC manaual install file from the Talend content provider, or the file must be made
available to this role at runtime.

This role is only known to work with Talend TAC 7.0.

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
nexus_archive: Artifact-Repository-Nexus-V3.9.0-01.zip
nexus_bin: Artifact-Repository-Nexus-3.9.0-01-unix/nexus-3.9.0-01/bin

nexus_version: 3
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
  hosts: "{{ dynamic_host | default('ec2_tag_name')}}"
  remote_user: root
  become: true
  gather_facts: yes

  roles:
   - tdye.talend-nexus3
```

License
-------

Apache License 2.0

Author Information
------------------

This role was created in 2018 by [Thomas A. Dye III, CCP](https://github.com/tdye).

