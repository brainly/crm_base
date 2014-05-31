crm_base
========

This role provides a bare Pacemaker&Corosync stack installation on Debian
(squeeze/wheeze) systems. Memberships betwean cluster members are provided
by the role as well.

Requirements
------------

The role was tested using Ansible 1.5 and higher. Corosync's keys should be
stored in Ansible's Vault so anything below 1.5 will not work. There are no
other dependencies.

Role Variables
--------------

This role requires:

- *crm_corosync_key* - this mandatory variable stores base64 encoded cluster
    key. It should be stored in Ansible-vault encrypted file.
- *crm_cluster_members* - this is a mandatory parameter defining the list of
    IPs of cluster members.

    It is stronly advised to assign the list of members of host's main group to
*crm_cluster_members* (either via 'vars:' stanza or direclty - by modyfing the
template. Corosync does not handle well assymetric memberships.

    In order to do it one will have to resolve inventory hostname to IP
addresses directly in the template. This can be done using one of the lookup
plugins freely available on the Internet.

Plese see Example Playbook section for details.

Dependencies
------------

This role may be used on its own provided that the user configures the cluster
resources manually. In case when full automation is desired, *crm_cluster* role
also needs to be used.

Example Playbook
-------------------------

Applying the role is straightforward:

```
- hosts: cluster_hosts
  vars:
    crm_cluster_members: ""{{ groups['cluster_hosts'] }}"
  roles:
    - crm_base
```

License
-------

Copyright 2014 Zadane.pl sp. z o.o.

Copyright 2014 Pawel Rozlach

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this role except in compliance with the License.
You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.


Author Information
------------------

This role has been created by Pawel Rozlach during the work time and spare time
at Zadane.pl and then opensourced by the company.

The *check_crm_v0_7* nrpe plugin has its own licensing and author information.
Please see the file contents for details.
