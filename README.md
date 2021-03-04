# Ansible boostrap script for openbsd

## Summary

this ansible playbook bootstraps a completely new installed openbsd.  
After the run everything is prepared for future ansible usage.

The following steps will be executed:
  * Python3 installation
  * default doas.conf for group wheel
  * admin user (non root) creation
  * add public key to the newly created user
  * change sshd_config to deny root logins and disable password authentication

## Variables used in this playbook

```yaml
admin_user: "<my admin username>"
# raw method is used with su or sudo depending on my use case - su for plain installations - sudo for vagrant
raw_method: "sudo|su"
pub_file: "<path to the public key file for the new admin user>"
```
These variables can be passed to the ansible-playbook command with the -e option or they can be written to a config file and initialized by the step ___Load additional variables from file___

## Example

### su
```bash
ansible-playbook -i ../inventory/inventory -u vagrant --ask-pass -b -K bootstrap_openbsd.yml -e"\
admin_user=automation \
raw_method=su  \
pub_file=../files/id_ed25519.pub"
```

### sudo
```bash
ansible-playbook -i ../inventory/inventory -u vagrant --ask-pass -b -K bootstrap_openbsd.yml -e"\
admin_user=automation \
raw_method=sudo  \
pub_file=../files/id_ed25519.pub"
```