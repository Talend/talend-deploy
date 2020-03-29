# tdye.talend-common

Requirements
------------

This role created directories that are required by the TAC role.

Role Dependencies
-----------------
None

Role Variables
--------------
None

Example Playbook
----------------

```yaml
- name: configure and deploy the TAC software to a node
  hosts: "{{ dynamic_host | default('ec2_tag_name')}}"
  remote_user: root
  become: true
  gather_facts: no

  roles:
   - tdye.talend-common
```

License
-------

Apache License 2.0

Author Information
------------------

This role was created in 2018 by [Thomas A. Dye III, CCP](https://github.com/tdye).

