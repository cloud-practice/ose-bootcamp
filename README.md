# About
This playbook prepares systems in the bootcamp lab to be installed with OpenShift. The actions performed are:
* subscription of systems
* installation of and update of software
* configuration of DNS server
* configuration of NFS server
* configuration of Docker and Docker Storage

# Assumptions

* The host running this playbook from is already subscribed and has ansible installed
* The hosts file will only be used to configure pre-requisites, NOT for the OpenShift install

# Setup

Setup the */etc/ansible/hosts* file (or use a custom file and point to it as the inventory file) with the following host groups (change the GUID value to match your environment):

```bash
[oselab]
oselab-GUID.oslab.opentlc.com

[ose]
master[00:02]-GUID.oslab.opentlc.com
node[00:01]-GUID.oslab.opentlc.com
infranode[00:01]-GUID.oslab.opentlc.com

[nfs]
nfs00-GUID.oslab.opentlc.com

[all:children]
oselab
ose
nfs
```

# Using

Set the variables for subscription-manager in *roles/pre_reqs/vars/main.yml* for *rhn_user* and *rhn_password* and call the *setup_environment.yaml* playbook:

```bash
ansible-playbook --forks=10 setup_environment.yaml"
```

Or call the playbook and specify the variables on the CLI:

```bash
ansible-playbook --forks=10 setup_environment.yaml --extra-vars="rhn_user=my.user rhn_password=my.password"
```
