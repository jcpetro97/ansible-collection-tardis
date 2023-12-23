# Rsyslog

Role for installing and configuring rsyslog.  

#### Variables

The only variables in this role are:

*BaseUrl*: This variable is used for the base git/github repo ( stored in a vars file in the playbook that calls this role)

*RsyslogConf*: the path to where in git the rsyslog config file is stored ( stored in a vars file in the playbook that calls this role)

#### Handlers

Once the new config is installed, a handler is called which restarts the rsyslog service

#### Sample Execution:

```
  roles:
     - role: Rsyslog
```