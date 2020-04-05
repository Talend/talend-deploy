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


## RJS download params
# Set download_talend to true to download install files from Talend content provider
#     for this to work, you must supply all information from your licensing email sent from Talend
# 
# For security purposes, these should be passed to ansible from the calling process
#
#talend_download: true
#talend_download_user: UUUU
#talend_download_pw: XXXXXx
#talend_download_url: http://www.opensourceetl.net/aaa/bbb_ccc/

#  The talend_install_path is the source directory for the RJS manual installer file.
#  This would be the enterprise manual installer for RJS downloaded from Talend.  Download links are sent with your license file.
#  If talend_download is false, then talend_install_path must point to the pre-downloaded Talend Manual install files
talend_rjs_install_path: /talend_install/downloads
talend_rjs_zip: Talend-JobServer-20180411_1414-V7.0.1.zip

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

