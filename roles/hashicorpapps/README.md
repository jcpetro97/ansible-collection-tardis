HashicorpApps
=============

Role to install the following applications by Hashicorp.  Packer, Vagrant, Vault, Terraform.

Requirements
------------

None

Role Variables
--------------

| Parameter                     | Choices / **Defaults**                       | Description                                |
| ----------------------------- | -------------------------------------------- | ------------------------------------------ |
| HashiCorpApps_Packer_State    | <ul><li>**present**</li><li>absent</li></ul> | Whether or not Packer will be installed    |
| HashiCorpApps_Vagrant_State   | <ul><li>**present**</li><li>absent</li></ul> | Whether or not Vagrant will be installed   |
| HashiCorpApps_Vault_State     | <ul><li>present</li><li>**absent**</li></ul> | Whether or not Vault will be installed     |
| HashiCorpApps_Terraform_State | <ul><li>present</li><li>**absent**</li></ul> | Whether or not Terraform will be installed |



Dependencies
------------

None

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

Install the default apps ( Vagrant and Packer )

```
- hosts: all
  become: true
  roles:
    - role: HashiCorpApps

```

Install only Vault

```
- hosts: all
  become: true
  gather_facts: yes
  roles:
    - role: HashiCorpApps
      vars:
        - HashiCorpApps_Packer_State: absent
        - HashiCorpApps_Vagrant_State: absent
        - HashiCorpApps_Terraform_State: present
```

License
-------

MIT

Author Information
------------------

* This role was created in 2022 by [John Petro](https://github.com/jcpetro97)