# Common role for Ansible Provision
## Description
This common role can be used on every single machine that is provisioned via ansible
- It updates cache if desired
- It installs some default packages
- It adds users and groups to servers

## Usage
To use this role you have to include it in your playbook
```
roles:
  - common
```

To make sure that all things getting done it is recommended, to include `vars_files` to your play. This gives you the possibility to use a different file with all play variables to set sufficient data and seperate logic and data.

# This role is devided into dfferent sections
1. Package management
2. System service management
3. User/Group management

All of this sections have different variables to configure the funtionality of them.

# OS Dependet variables
You can find OS dependent packages in vars/ directory.

# Package management

## Usage
`common_update_cache: **True**|False`
Enable/Disable upgrading only the system package managers cache to be sure that you get latest packages.
`common_upgrade_system: **True**|False`
Enables upgrading the complete system.
```
common_install_packages:
  - firefox
  - aws-cli
```
List of packages to be installed by this role.
```
common_remove_packages:
  - python2
```
List of packages to removed by this role.

# System services manager
```
common_enable_services:
  - NetworkManager
```
Starts and enables services that you specifie.
```
common_disable_services
```
Stops and disables services that you specifie.

# User and Group manager
Add local groups and users
:Exclamation: It is important to use `local_groups` before adding user with `local_users` to a new group.

**Awsome Feature** provisions shell environments form github.com if desired.

*Complete Example:*

Add local groups:
```
common_local_groups:                                     # Dictionary name used by role
  $group_name:                                    # Groupname to be added
    gid: $gid_number                              # Free GID for group
  $group_name2:
    gid: $gid_number2
```

Add local users:
```
common_local_users:                                      # Dictionary name used by role
  $username:                                      # Username to be added
    uid: $uid_number                              # Free UID for user
    comment: Provision User                       # Set comment to user, this is optional
    groups: "$group1,$group2"                     # Comma seperated list of groups
    git_repo: "http://github.com/dthielking/dots" # git repositor where dots are located
    git_version: master                           # Defautls to HEAD version
    authorized_key: "ssh-rsa $key key@key.com
  $username2:
    uid: $uid_number2
    groups: "group1"
```
