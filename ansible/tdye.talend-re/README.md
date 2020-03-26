# tdye.talend-re

Requirements
------------

This role installs a single copy of the Talend Remote Engine for Talend Cloud server on a compute node or VM

A mount point called '/talend_install' is required where the Talend manual install files for the RE is stored.

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


# RE params
talend_re_install_path: /talend_install/Manual_Installation/RE
talend_re_zip: Talend-RemoteEngine-V2.4.0-108.tar

pairing_key: 01234567899999999
pairing_service_url:  https://pair.eu.cloud.talend.com     # uncomment the pairing service for your region/account
#pairing_service_url:  https://pair.us.cloud.talend.com
#pairing_service_url:  https://pair.ap.cloud.talend.com
```

Dependencies
------------
JDK 1.8 must be preinstalled  
JAVA_HOME must be set before install 

Example Playbook
----------------

```yaml
- name: configure and deploy the Remote Engine software to a node
  hosts: all
  remote_user: root
  become: true
  gather_facts: yes
  environment:
    JAVA_HOME: /usr/java/latest

  roles:
   - tdye.talend-re
```

License
-------

Apache License 2.0

Author Information
------------------

This role was created in 2019 by [Thomas A. Dye III, CCP](https://github.com/tdye).

