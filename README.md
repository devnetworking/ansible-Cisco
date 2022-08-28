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


## Use

### Using vars_files

First, define a `credentials.yml` ([example](https://github.com/emzaden/ansible-Cisco/blob/main/playbooks/credentials.template)) file where you specify your Cisco ISE credentials as ansible variables:
```
---
cisco_hostname: <A.B.C.D>
cisco_username: <username>
cisco_password: <password>
```

Create a `hosts` ([example](https://github.com/emzaden/ansible-Cisco/blob/main/playbooks/hosts)) file that uses `[cisco_servers]` with your Cisco Settings:
```
[cisco_nodes]
cisco_node
```

Then, create a playbook `myplaybook.yml` referencing the variables in your credentials.yml file and specifying the full namespace path to the module, plugin and/or role:
```
- hosts: cisco_servers
  vars_files:
    - credentials.yml
  gather_facts: no
  tasks:
  - name: Get network device by id
    cisco.network_device_info:
      cisco_hostname: "{{cisco_hostname}}"
      cisco_username: "{{cisco_username}}"
      cisco_password: "{{cisco_password}}"
```

Execute the playbook:
```
ansible-playbook -i hosts myplaybook.yml
```
In the `playbooks` [directory](https://github.com/emzaden/ansible-Cisco/tree/main/playbooks) directory you can find more examples and use cases.

**Note**: The examples found on the `playbooks` directory use the `group_vars` variables. Remember to make the appropiate changes when running the examples.

### Using group_vars directory

First, define your group_vars for credentials `cisco_servers` ([example](https://github.com/emzaden/ansible-Cisco/blob/main/playbooks/group_vars/node_servers)) file where you specify your Cisco NODE credentials as ansible variables:
```
---
cisco_hostname: <A.B.C.D>
cisco_username: <username>
cisco_password: <password>
```

Create a `hosts` ([example](https://github.com/emzaden/ansible-Cisco/blob/main/playbooks/hosts)) file that uses `[Node_servers]` with your Cisco Node Settings:
```
[Node_servers]
Node
```

Then, create a playbook `myplaybook.yml` ([example](https://github.com/emzaden/ansible-Cisco/blob/main/playbooks/network_device.yml)) referencing the variables in your `group_vars/cisco_servers` file and specifying the full namespace path to the module, plugin and/or role:
```
- hosts: cisco_servers
  gather_facts: no
  tasks:
  - name: Get network device by id
    cisco.network_device_info:
      cisco_hostname: "{{cisco_hostname}}"
      cisco_username: "{{cisco_username}}"
      cisco_password: "{{cisco_password}}"
```

Execute the playbook:
```
ansible-playbook -i hosts myplaybook.yml
```
In the `playbooks` [directory](https://github.com/emzaden/ansible-Cisco/tree/main/playbooks)  directory you can find more examples and use cases.

**Note**: The examples found on the `playbooks` directory use the `group_vars` variables. Consider using `ansible-vault` to encrypt the file that has the `cisco_username` and `cisco_password`.


## Update
Getting the latest/nightly collection build

Clone the ansible-ise repository.
```
git clone https://github.com/emzaden/ansible-Cisco.git
```

Go to the ansible-ise directory
```
cd ansible-ise
```

Pull the latest master from the repo
```
git pull origin master
```

Build and install a collection from source
```
ansible-galaxy collection build --force
```

### See Also:

* [Ansible Using collections](https://docs.ansible.com/ansible/latest/user_guide/collections_using.html) for more details.


