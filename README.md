# Common role for Ansible Provision
## Description
This common role must be used on every single server that is provisioned via ansible
- It installs some default packages
- It adds users and groups to servers

## Usage
To use this role you have to include it in your playbook
```
roles:
  - common
```

To make sure that all things getting done it is recommended, to include `vars_files` to your play. This gives you the possibility to use a different file with all play variables to set sufficient data and seperate logic and data.

There are some optional Variables that could be used to get things done:
- provisioned    [scalar]
- packages       [list]
- local_users    [dictionary]
- local_groups   [dictionary]

# Variable usage

Set server as provisioned or not
`provisioned: True|False`

Install default packages
```
packages:
  - package1
  - package2
  - package3
```

Add local groups and users
:Exclamation: It is important to use `local_groups` before adding user with `local_users` to a new group
*Complete Example:*

Add local groups:
```
local_groups:                                     # Dictionary name used by role
  $group_name:                                    # Groupname to be added
    gid: $gid_number                              # Free GID for group
  $group_name2:
    gid: $gid_number2
```

Add local users:
```
local_users:                                      # Dictionary name used by role
  $username:                                      # Username to be added
    uid: $uid_number                              # Free UID for user
    groups: "$group1,$group2"                     # Comma seperated list of groups
    git_repo: "http://github.com/dthielking/dots" # git repositor where dots are located
  $username2:
    uid: $uid_number2
    groups: "group1"
```
