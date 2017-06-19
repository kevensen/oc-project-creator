oc-project-creator
=========

This role creates a project, assigns the designated user as a the project admin (this is configurable), and applies quota in an OpenShift Container Platform cluster.

Requirements
------------

At least one operational OpenShift Container Platform cluster.

kevensen.oc

Role Variables
--------------

The following variables are the defaults for a project and are found in defaults/main.yml.
```
# Hard quota for the number of pods allowed in a project
pod_quota: 10

# Hard quota for the number of services allowed in a project
service_quota: 10

# Hard quota for the number of replication controllers allowed in a project
rc_quota: 10

# Hard quota for the number of secrets allowed in a project
secret_quota: 10

# Hard quota for the number of persistent volume claims allowed in a project
pvc_quota: 10

# The role applied to the user who will "own" the project
project_role: admin
```

The following variables should be set as parameters
```
# The name of the project to be created
project_name: ansibletest

# The display name of the project to be created
project_display_name: Ansible Test

# The description of the project to be created
project_description: This is an Ansible Test

# The username of the user who will "own" the project.
user_name: ansibleuser

# Whether or not to validate the TLS certs of the API endpoint
validate_certs: true

# The token of the service account with which to access the API
ansible_sa_token: abcdefg
```

Dependencies
------------

This role requires the kevensen.oc role to be applied to a host as well.

Example Playbook
----------------

The following example shows how one can use this role to create a project.
```
# file: oc-create-project.yml
- hosts: oc
  roles:
  - kevensen.oc
  - kevensen.oc-project-creator
  vars:
    ansible_become: true
    project_name: myreallycoolproject
    project_display_name: My Really Cool ProjectRequest
    project_description: This really cool OpenShift project was created by Ansible.
    ansible_sa_token: absdefg
    validate_certs: false
```
License
-------

GPLv3

Author Information
------------------

Ken Evensen is a Solutions Architect with Red Hat
