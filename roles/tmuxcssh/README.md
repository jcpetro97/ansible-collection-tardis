TmuxCsshInstall
===============

This is an ansible role that pulls tmux-cssh from github, and installs it into a bin directory inside the users home directory.

Requirements
------------

The user account referenced in the UserName variable must exist. 

Role Variables
--------------

* **Users:** Used for Loop Control
* **UserName:** The user environment where tmux-cssh will be installed. ( user must already exist )
* **TmuxCsshUrl:** url of the github repo for tmux-cssh 

Usage
-----

If the variables are stored in a vars file:

```
	roles:
		- TmuxCsshInstall
      vars:
        Users:
          - UserName: testuser1
          - UserName: testuser2
```

Notes
-----
* Changes to the variables can be done at the playbook, hostvar or at execution time.

License
-------

MIT / BSD

Author Information
-------------------

- 10/4/2020 - John Petro
- 8/19/2022 - Updated to Version 2