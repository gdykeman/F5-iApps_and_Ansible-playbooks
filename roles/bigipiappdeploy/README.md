# bigip-ansible-deploy-iapp
Ansible role to deploy an F5 iApp

This is a workflow to
*  Deploy an iApp

Playbook steps
* Take a template file as input and create a JSON payload, substitute the VIP and pool member IP values from the variable file
* Deploy the iApp using the JSON payload above (iApp template in this case is already present on the BIG-IP)
  - Template used here is f5.http iapp

## Requirements
* This role requires Ansible 2.4
* BIG-IP is licensed
* Packages to be installed
  - pip install f5-sdk
  - pip install bigsuds

## Role Variables
The variables that can be passed to this role and a brief description about them are as follows.

```
directory_path: "/root/playbooks/roles/deploy_iapp/templates"   //provide your directory path here
bigip_address: "xx.xx.xxx.xxx"                                  //provide your BIG-IP IP address/hostname
username: "admin"
password: "admin"

vip_ip: "10.168.68.143"

```

## Example Playbook
```
- hosts: localhost
  gather_facts: false
  roles:
  - { role: f5devcentral.bigip-ansible-deploy-iapp }

```

## Sample inventory file

```
[webserver]
192.168.68.140
192.168.68.141

```

## Credential storage

Because this role includes usage of credentials to access your BIG-IP, I recommend that you supply these variables in an ansible-vault encrypted file.

This can be supplied out-of-band of this role

Steps:
- Store your vault password in a file - '~/.vault_pass.txt'
- Execute playbook as follows - ansible-vault encrypt <<variable_filename>> --vault-password-file ~/.vault_pass.txt

For more information refer to: http://docs.ansible.com/ansible/latest/playbooks_vault.html

## Certificate validation
To validate the SSL certificates of the BIG-IP REST API
- set validate_certs: true
- Generate a public private key pair
- Store the public key on BIG-IP (https://support.f5.com/csp/article/K13454#bigipsshdaccept)

## Credits
https://github.com/F5Networks/f5-ansible
