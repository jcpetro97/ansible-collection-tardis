Ansible Role: Users
===================

This role manages users and their groups on your system.

Requirements
------------


Role Variables
--------------

These defaults are set in `defaults/main.yml`:
```yaml
---
# defaults file for users

# The default value, whether to create a group for every user
# and make that their primary group
users_group_per_user: yes
# If no group per user is created, then this is the default primary
# group all users belong to
users_group: users
# The default value, whether to create home directory for the user
# when the account is created or if the home directory does not exist
users_create_home: yes
# The default sudo options for the user when sudo is set to yes,
# but none are specified
users_sudo_options: "ALL=(ALL) NOPASSWD: ALL"
# The default shell for the user when none is specified
users_shell: /bin/bash

# Lists of users to create, remove or modify
users: []

# List of user groups to create or delete
users_groups: []

```
A good place to put replacements for these variables is in `group_vars/all` or `group_vars/group_name`,
if you only want defined users and groups to be on certain machines.

The `users` variable containing the list of users to create, remove or modify.
Each user in this list is defined as an dictionary.
The following parameters are available for each user dictionary:

| User Parameter | Choices / **Defaults** | Comments |
|---|---|---|
| `name` *required* || Name of the user to create, remove or modify. |
| `state` | Choices:<ul><li>**present**</li><li>absent</li></ul> | Whether the account should exist or not, taking action if the state is different from what is stated. |
| `comment` || Optionally sets the description (aka GECOS) of user account. |
| `uid` || Optionally sets the UID of the user. |
| `group` | Default: **`user.name`** | Optionally overrides the user's primary group taken from `users_group_per_user=yes` or `users_group` (takes a group name). |
| `gid` || This only affects `users_group_per_user=yes`. Optionally sets different GID of user's primary group. Otherwise the UID will be used. |
| `groups` || List of groups user will be added to. When set to an empty string the user is removed from all groups except the primary group. |
| `append` | Choices:<ul><li>**no**</li><li>yes</li></ul> | If *yes*, add the user to the groups specified in `groups`. If *no*, user will only be added to the groups specified in `groups`, removing them from all other groups. |
| `password` | Default: **!**| Optionally set the user's password to this crypted value. Otherwise the user account will be locked. |
| `update_password` | Choices:<ul><li>**always**</li><li>on_create</li></ul> | *always* will update passwords if they differ. *on_create* will only set the password for newly created users. |
| `create_home` | Choices:<ul><li>**yes**</li><li>no</li></ul> | Optionally overrides this value taken from `users_create_home`. Unless set to *no*, a home directory will be made for the user when the account is created or if the home directory does not exist. |
| `home` | Default: **/home/`user.name`** | Optionally set the user's home directory. |
| `shell` | Default: **/bin/bash** | Optionally overrides the user's shell taken from `users_shell`. |
| `sudo` | Choices:<ul><li>**no**</li><li>yes</li></ul> | If *yes*, set the user's sudo options taken from `user.sudo_options`. Otherwise, remove the user's sudo options. |
| `sudo_options` | Default: **ALL=(ALL) NOPASSWD: ALL**| Optionally overrides the user's sudo options taken from `users_sudo_options`. |
| `remove` | Choices:<ul><li>**no**</li><li>yes</li></ul> | This only affects `user.state=absent`, it attempts to remove directories associated with the user. The behavior is the same as *userdel --remove*, check the man page for details and support. |
|`force` | Choices:<ul><li>**no**</li><li>yes</li></ul> | This only affects `user.state=absent`, it forces removal of the user and associated directories on supported platforms. The behavior is the same as *userdel --force*, check the man page for details and support. |

The `users_groups` variable containing the list of user groups to create or delete. Each group in this list is defined as an dictionary.
The following parameters are available for each group dictionary:

| Group Parameter | Choices / **Defaults** | Comments |
|---|---|---|
| `name` *required* || Name of the group to manage. |
| `state` | Choices:<ul><li>**present**</li><li>absent</li></ul> | Whether the group should be present or not on the remote host. |
| `gid` || Optional GID to set for the group. |


Dependencies
------------

No Dependancies

Example Playbook
----------------

```yaml
---
- name: testhost
  hosts: all
  gather_facts: no
  become: yes

  roles:
    - role: UserManage
      vars:
        users_groups:
          - name: foo
          - name: bin
        users:
          - name: nouser
            comment: No User
            create_home: no
          - name: administrator
            comment: Administrator
            uid: 2002
            groups: [foo,bin]
            cron: yes
            sudo: yes
          - name: user
            comment: User
            uid: 2003
            groups: [users,foo,bin]
            shell: /bin/sh
```

Author Information
------------------

- [Robert de Bock](https://robertdebock.nl/) <robert@meinit.nl>
- [Brian Rimek](https://github.com/rembik)
- John Petro