
# Ansible Role: jenkins-habilitation

This Ansible role for jenkins habilitation .

## Requirements

* lxml > 2.3

* Ansible version > 2.3

* Plugin : Role Strategy plugin

## Role Variables

    jenkins_config_file: /home/admin/.jenkins/config.xml

jenkins config file is the jenkins root configuration

**rolesMaps** : A list of roles maps and the directives to use for creation and updating roles.
* type : the type of roleMap
* roles : list of roles
* name : the attribute name of role
* projectName: represent the name of your project and the directory where should you put your jobs
* permissions : list of permissions
  * permission : the value of permission
* assisgnedSIDs : list of usernames
  * sid : the username

all_permissions : assigns all permissions to a role

standard_permissions : gathers a necessary permission set for a project

users_mikasa_raiser: defined set of users to assign to the project 'mikasa'

```

roleMaps:
  - roleMap:
    type: globalRoles
    roles:
      - name: admin
        permissions:
          "{{ all_permissions }}"
        assignedSIDs:
          - sid: "admin"
      - name: anonymous
        permissions:
          - permission: hudson.model.Hudson.Read
        assignedSIDs:
          - sid: "user_test"
```       

to add a new project you have to specify roleMap 'projectRoles' and give the name and the pattern of the new role with permissions and assigned users if necessary

Here is an example to illustrate the addition of a new project named 'myproject' while assigning users user1 and user2 with admin rights on the project

```
roleMaps:
  - roleMap:
    type: projectRoles
    roles:
      - name: myproject.admin
        projectName: myproject
        permissions:
          "{{ standard_permissions }}"
        assignedSIDs:
          "{{ users_myproject }}"

```


## Dependencies

## Example Playbook

    - hosts: all
      roles:
        - { role: ansible-role-jenkins-habilitation }

## License

BDSI

## Author Information

This role was created in 2018 by [CHRIFI ALAOUI Hakim](https://github.com/Hakimo003/ansible-role-jenkins-habilitation)
