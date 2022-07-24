[![CI](https://github.com/de-it-krachten/ansible-role-acl/workflows/CI/badge.svg?event=push)](https://github.com/de-it-krachten/ansible-role-acl/actions?query=workflow%3ACI)


# ansible-role-acl

Manages POSIX ACL on supported systems


## Platforms

Supported platforms

- Red Hat Enterprise Linux 7<sup>1</sup>
- Red Hat Enterprise Linux 8<sup>1</sup>
- Red Hat Enterprise Linux 9<sup>1</sup>
- CentOS 7
- RockyLinux 8
- RockyLinux 9
- OracleLinux 8
- AlmaLinux 8
- AlmaLinux 9
- Debian 10 (Buster)
- Debian 11 (Bullseye)
- Ubuntu 18.04 LTS
- Ubuntu 20.04 LTS
- Ubuntu 22.04 LTS
- Fedora 35
- Fedora 36

Note:
<sup>1</sup> : no automated testing is performed on these platforms

## Role Variables
### defaults/main.yml
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



## Example Playbook
### molecule/default/converge.yml
<pre><code>
- import_playbook: converge-pre.yml

- name: sample playbook for role 'acl'
  hosts: all
  become: "{{ molecule['converge']['become'] | default('yes') }}"
  vars:
    acl_list: [{'path': '/srv/shares/share1/group1', 'group': 'group1', 'perms': 'rwx'}, {'path': '/srv/shares/share1/group1', 'group': 'group2', 'perms': 'r-x'}, {'path': '/srv/shares/share1/group1', 'group': 'group3', 'perms': '---'}, {'path': '/srv/shares/share1/group2', 'group': 'group2', 'perms': 'rwx'}, {'path': '/srv/shares/share1/group2', 'group': 'group1', 'perms': 'r-x'}]
  tasks:
    - name: Include role 'acl'
      include_role:
        name: acl
</pre></code>
