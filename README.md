# Kibana (+support RHEL, validate user/group)

This project is a fork for: [Ansible-Galaxy-Stouts](https://github.com/Stouts/Stouts.kibana)

## We add this validation:

### 1.- `To validate first if the user/group {kibana_user}. {kibana_group}.`
```yaml
---
- name: install - create group
  group:
    name: "{{ kibana_group }}"
    system: yes
    state: present
  sudo: yes

- name: install - create user
  user:
    name: "{{ kibana_user }}"
    group: "{{ kibana_group }}"
    home: "{{ kibana_home }}"
    createhome: no
    shell: /bin/false
    system: yes
    state: present
  sudo: yes
```

### 2.- `We add an example about how do we could use the role "ansible-role-kibana-ds".`
/ansible-role-kibana-ds/tree/master/examples/site_playbook_kibana_role.yml

```yaml
---
- hosts: localhost
  roles:
    - role: ansible-role-kibana-ds
  vars:
    - kibana_version: 4.1.1
    - kibana_os_version: linux-x64
    - kibana_home: /var/www/kibana
    - kibana_user: www-data-elastic
    - kibana_group: www-data-elastic
    - kibana_port: 8004
    - inventory_elastic_hostname: localhost
    - inventory_elastic_port: 8010
---
