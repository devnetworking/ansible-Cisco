# Ansible Collection - cisco automation

## Ansible Modules for Cisco 

The ise-ansible project provides an Ansible collection for managing and automating your Cisco environment. It consists of a set of modules and roles for performing tasks related to Cisco node.

This collection has been validated with Cisco 15.9(3)M / August 15, 2019.

These Ansible modules will work with any version of Cisco that supports the underlying REST API resources you want to configure. Please see the [Cisco Automation](https://www.cisco.com/c/en/us/solutions/automation/network-automation.html) reference for which REST Resources were first supported in which Cisco Version.

*Note: This collection may be is not compatible with versions of Ansible before v2.9.*

## Requirements
- Ansible >= 2.9
- Python >= 3.6, as the Cisco ISE SDK doesn't support Python version 2.x
- requests >= 2.25.1, for the personas modules and personas_deployment role.

## Install
Ansible must be installed ([Install guide](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html))
```
sudo pip install ansible
```

networking-cisco 7.0.0 must be installed
```
sudo pip install networking-cisco
```

Install the collection ([Galaxy link](https://galaxy.ansible.com/cisco/ios))
```
ansible-galaxy collection install cisco.ios
```


