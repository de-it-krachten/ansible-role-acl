[![CI](https://github.com/de-it-krachten/ansible-role-acl/workflows/CI/badge.svg?event=push)](https://github.com/de-it-krachten/ansible-role-acl/actions?query=workflow%3ACI)


# ansible-role-acl

WRITE HERE


Platforms
--------------

Supported platforms

- CentOS 7
- CentOS 8
- Debian 10 (Buster)
- Debian 11 (Bullseye)
- Ubuntu 18.04 LTS
- Ubuntu 20.04 LTS



Role Variables
--------------
<pre><code>
# package needed to make (NFSv4) ACLs work
acl_packages:
  - acl
  - nfs4-acl-tools

# User / group to change paths to
acl_default_user: ''
acl_default_group: ''

# Use NFSv4 over POSIX ACLS
acl_use_nfsv4: false
</pre></code>


Example Playbook
----------------

<pre><code>
- name: Converge
  hosts: all
  vars:
    acl_list:
      - path: /srv/shares/share1/group1
        group: group1
        perms: rwx
      - path: /srv/shares/share1/group1
        group: group2
        perms: r-x
      - path: /srv/shares/share1/group1
        group: group3
        perms: ''
      - path: /srv/shares/share1/group2
        group: group2
        perms: rwx
      - path: /srv/shares/share1/group2
        group: group1
        perms: r-x
  tasks:
    - name: Create groups
      group:
        name: '{{ item }}'
      loop:
        - group1
        - group2
        - group3
    - name: Include role 'ansible-role-acl'
      include_role:
        name: ansible-role-acl
</pre></code>
