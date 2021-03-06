sudo
=========

This role can manage both /etc/sudoers and any file in /etc/sudoers.d
by default the role will NOT making any changes unless the variable
sudo_sudoers or sudo_sudoers_d is defined.


Basic help for managing sudoers:

[help.ubuntu.com/community/Sudoers](https://help.ubuntu.com/community/Sudoers)


Role Variables
--------------
`sudo_sudoers`     (REQUIRED)

The role expect a relative or full path to the main sudoers file.


`sudo_sudoers_d`   (OPTIONAL)

Optionally sudo_sudoers_d can be a path to the directory with additional config files.
All of the files from this path will be copied to remote and VALIDATED using
the visudo command prior the actual placement.


NOTE: all files copied by the template module hence can include magic
      variables like {{ ansible_managed }} at the top of the file.


Example
----------------

Play on all nodes

```
- hosts: all
  roles:
   - sudo
```

For example it is advised to host the actual files along side with the ansible
repo that can look something like this:


```
group_vars/all.yml
 sudoers: group_files/all/sudo/sudoers

group_vars/us-east-1a-myapp.yml
 sudoers_d: group_files/us-east-1a-myapp/sudo/sudoers.d

group_files/us-east-1a-myapp/sudo/sudoers.d
└── sudoers.d
    ├── bob
    └── sponge
```

In general the sugested structure for the raw files can be something like:

```
group_files/<group_name>/<role_name>
hosts_files/<host_name>/<role_name>
```

Author Information
------------------

Tal Lannder

tal@pjili.org
