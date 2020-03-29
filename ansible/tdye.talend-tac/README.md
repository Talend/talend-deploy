# tdye.talend-tac

Requirements
------------

A mount point called '/talend_install' is required where the Talend manual install files for TAC and the
TAC JDBC driver jar file are stored.

A Talend supported RDMBS must exist and have a database created for TAC's use.

This role should build a TAC for Talend enterprise releases 6.2 to 7.2.

Role Dependencies
-----------------

A suitable Oracle JVM must be preinstalled before this role is called.

[ChristopherDavenport.universal-tomcat](https://galaxy.ansible.com/ChristopherDavenport/universal-tomcat/)

Role Variables
--------------

```yaml
# defaults file for tdye.talend-tac
# talend_root is the installation destination for TAC
talend_root: /opt/talend-7.2.1
talend_version: 7.2.1

# talend_user and group are the Linux owner and group name of the TAC filesystem
talend_user: talenduser
talend_group: talendgroup


##########################################################################################################
# Set download_talend to true to download install files from the Talend content provider.
#     For this to work, you must supply all information from your licensing email sent from Talend
#
# These should be passed into this role from an external (calling) source (Vagrant, Terraform, ENV, etc.).  
# Uncomment if needed
#
#talend_download: true
#talend_download_user: 
#talend_download_pw: 
#talend_download_url:                                 # URLs may be different, check your licensing email
# 
##########################################################################################################

# The talend_install_path is the source directory for the TAC manual installer file.
# This would be the enterprise manual installer for TAC downloaded from Talend.  Download links are sent with your license file.
# If talend_download is false, then talend_install_path must point to the predownloaded Talend Manual install files
talend_install_path: /talend_install/Manual_Installation/TAC

# talend_tac_zip is the name of the manual installer file for TAC.  It will be a zip file.
talend_tac_zip: Talend-AdministrationCenter-XXXXXXXXXXXXXX-V7.0.1.zip

# TAC Database parameters
tac_db_url: jdbc:mariadb://localhost:3306/tac_721
tac_db_username: talend
tac_db_password: talend
tac_db_jdbc_path: /talend_install/Manual_Installation/files
tac_db_jdbc_driver: mariadb-java-client-2.2.2.jar

#Tomcat params
tomcat_version: 8.0.42
tomcat_use_java: false
java_home: /usr/java/default
tomcat_use_apr: false
tomcat_user_name: talenduser
tomcat_user_group: talendgroup


# a mount point that contains the installation source is required.  Currently it must be mounted to '/talend_install'
# if you are building TAC in Azure, you can use the Azure File Storage system to provide the install files.
# This must be created beforehand, and populated with the Talend manual installer files beforehand.
# File path for the manual installer files must conform to other path variables for this role.

# set azure_vm to true to enable this feature.  Be sure the other variables have valid values

# Azure FS parameters
#
azure_vm: true
az_username: XXXXX
az_password: YYYYY
az_src: //XXXXXXXXXX.file.core.windows.net/tac
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
   - tdye.talend-tac
```

License
-------

Apache License 2.0

Author Information
------------------

This role was created in 2018 by [Thomas A. Dye III, CCP](https://github.com/tdye).

