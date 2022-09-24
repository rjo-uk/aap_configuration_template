# Ansible Automation Platform Configuration as Code examples template

Is is a combination of all the Red Hat CoP Config as Code collections to deploy and configure AAP. This is built for multi environment (meaning multiple AAP instances/clusters). If you want an object across all environments put it in the correct file/list under the all group. If there is a specific object for only one environment then put it under that environments folder[^1].

[^1]: If you only have/want one environment you could delete dev/test/prod folders in group_vars and remove all the _all added to vars in all group.

You will need to replace the vault files with your own with these variables:

```yaml
---
cloud_token: 'this is the one from console.redhat.com'
offline_token: 'this is the one linked below about api token'
rh_username: 'redhat user login (this is used to attach your subs to controller)'
rh_password: 'password for redhat account'
root_machine_pass: 'password for root user on builder (if not root user more changes will need to be made)'
ah_api_user_pass: 'this will create and use this password can be generated'
controller_api_user_pass: 'this will create and use this password can be generated'
controller_pass: 'admin account pass for controller, if none is given it will default to Password1234!'
ah_pass: 'hub admin account pass, if none is given it will default to Password1234!'
ah_token_password: "{{ ah_api_user_pass }}"
vault_pass: 'the password to decrypt this vault'
...
```

**_NOTE:_** Do not forget to update your inventory files replacing the `HERE` lines, if you do not have a `builder` server you can use `hub` for this. Also update `scm_url` in `group_vars/all/projects.yml` with your git URL.

## controller config

`ansible-playbook -i inventory_dev.yml -l dev playbooks/controller_config.yml --ask-vault-pass`

## automation hub config

`ansible-playbook -i inventory_dev.yml -l dev playbooks/hub_config.yml --ask-vault-pass`

## custom ee

currently doesn't work in CLI, expected to be run in Controller

## custom collections

currently doesn't work in CLI, expected to be run in Controller

## aap utilities (aap installer)

`ansible-playbook -i inventory_dev.yml playbooks/install_aap.yml --ask-vault-pass`

Acquire your token at [redhat api](https://access.redhat.com/management/api/) see [access article](https://access.redhat.com/articles/3626371)

## install and configure

`ansible-playbook -i inventory_dev.yml -l dev playbooks/install_configure.yml --ask-vault-pass -e "env=dev"`

Acquire your token at [redhat api](https://access.redhat.com/management/api/) see [access article](https://access.redhat.com/articles/3626371)
