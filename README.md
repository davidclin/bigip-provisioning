## Last updated: 10/9/2017


# bigip-provisioning (and tags)
Ansible role to automate provisioning tasks on a BIG-IP. 
The role will perform the following
* Configure VLANs                        (vlans)
* Configure Self-IPs                     (selfips)
* Create nodes                           (nodes)
* Create pool                            (pool)
* Create SNAT pool                       (snatpool)
* Assign members to pool and SNAT pool   (addtopool)
* Create a HTTPS virtual server          (virtualserver)

## Requirements
* This role requires Ansible 2.4
* BIG-IP is licensed
* Packages to be installed
  - pip install f5-sdk
  - pip install bigsuds
  - pip install netaddr

## Role Variables
The variables that can be passed to this role and a brief description about them are as follows.

```
username: <username>                                //BIG-IP username
password: <password>                                //BIG-IP password

```

## Example Playbook
```
- hosts: bigips
  gather_facts: false
  roles:
  - { role: bigip-provisioning }

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
