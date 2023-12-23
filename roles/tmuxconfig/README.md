TmuxConfig
==========

This role was written to copy the tmux config into place.  ( /home/username/.tmux.conf)
If the username is jxpsys, and the location is Work, then it will copy the .tmux.startup to the home directory as well

If the username is my `work username`, and `TmuxStartup` == `yes` then a `.tmux.startup` file specific to my work settings will be copied.  Otherwise a `.tmux.startup` with non-work specific settins will be copied. 

Role Variables
--------------

| Parameter | Choices | Comments |
| --------- | ------- | -------- |
| `UserName`| | Username where config will be copied to|
| `TmuxStartup` | Choices:<ul><li>yes</li><li>**no**</li></ul> |Set to yes if you want the .tmux.startup copied into the homedir.  Selecting no will not copy the file|
| `PrimaryGroup` | User Defined | Set group ownership to a group other than `users` |

Dependencies
------------

None

Example Playbook
----------------

```
roles:
  - {role: TmuxConfig, UserName: "testuser", TmuxStartup: "yes"}

roles:
  - role: TmuxConfig
    vars:
      UserName: "testuser"
      TmuxStartup: "yes"

```

License
-------
MIT

Author Information
------------------

* This role was created in 2020 by [John Petro](https://github.com/jcpetro97)
* Code updated to V2 in 8/2022