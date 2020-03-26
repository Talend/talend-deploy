# tdye.talend-ci

Requirements
------------
A mount point called '/talend_install' is required where the Talend manual install files for all components
of CI:  
    Talend CommandLine (Talend Studio)  
    Talend CI Builder Maven Extensions  
    Talend Cloud Publisher Maven Extensions (optional)  

This role should build a Talend CI VM for Talend and Talend Cloud enterprise release 7.0.

This role works with Nexus releases 2 and 3.  The role detects the version of Nexus and configures itself on install.

Role Dependencies
-----------------

A suitable Oracle JDK must be preinstalled before this role is called.  (JDK 1.8)

Role Variables
--------------

```yaml
talend_root: /opt/talend-7.0.1
talend_version: 7.0.1

talend_user: vagrant
talend_group: vagrant

epel_repo_url: "https://dl.fedoraproject.org/pub/epel/epel-release-latest-{{ ansible_distribution_major_version }}.noarch.rpm"
epel_repo_gpg_key_url: "https://dl.fedoraproject.org/pub/epel/RPM-GPG-KEY-EPEL-{{ ansible_distribution_major_version }}"
epel_repofile_path: "/etc/yum.repos.d/epel.repo"


# CI Builder params
talend_ci_install_path: /talend_install/Manual_Installation/CI-Builder
talend_ci_zip: Talend-CI-Builder-2018XXXX_XXXX-V7.0.1.zip

# nexus params
nexus_user: admin
nexus_password: Talend123
nexus_server: xxx.xxx.xxx.xxx
nexus_port: 8081


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
JDK 1.8  
Nexus 2 or 3


Example Playbook
----------------

```yaml
- name: configure and deploy the Talend CI software to a node
  hosts: all
  remote_user: root
  become: true
  gather_facts: yes

  roles:
   - tdye.talend-ci
```

License
-------

Apache License 2.0

Author Information
------------------

This role was created in 2018 by [Thomas A. Dye III, CCP](https://github.com/tdye).

