# InstallStandardPackages.yml

Installs the standard packages that I usually require for my desktop or servers.  These are packages that are out of the default repos, nothing added.  

#### Role Variables

|Variable Name|System Types |Description|
|-------------|-------------|-----------|
|SystemType|Choices:<ul><li>**Server**</li><li>Desktop</li></ul> | Defines the system type so the proper packages can be installed| 

#### Usage Instructions:

Packages will be taken from the vars/main.yml file.  If packages need to be added, edit that file.

**NOTE:** I kept the virtualbox package out of the list, so that I could test the install on a virtual machine.

To run the playbook, include this role in the top level playbook

Ex1. This is for a Server install

```
- hosts: localhost
  become: true

  roles:
      - {role: InstallStandardPackages}

```

Ex2. This is for a Desktop install

```
- hosts: localhost
  become: true

  roles:
      - {role: InstallStandardPackages, SystemType: 'Desktop'}

```