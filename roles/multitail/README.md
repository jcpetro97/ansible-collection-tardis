# Multitail

This role will be used to configure multitail.  The role will peform the following tasks

* Make sure multitail is installed (will install it if it isn't)
* It will add some customizations into the /etc/multitail.conf file for fail2ban, sudo, ssh and rsnapshot
* It will add an alias into the .bashrc for users that are defined 

#### Example Role Execution

```
	roles:
		- Multitail
```