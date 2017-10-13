<pre>
 _     _       _                                        
| |__ (_) __ _(_)_ __                                   
| '_ \| |/ _` | | '_ \                                  
| |_) | | (_| | | |_) |                                 
|_.__/|_|\__, |_| .__/                                  
         |___/  |_|                                     
                      _     _             _             
 _ __  _ __ _____   _(_)___(_) ___  _ __ (_)_ __   __ _ 
| '_ \| '__/ _ \ \ / / / __| |/ _ \| '_ \| | '_ \ / _` |
| |_) | | | (_) \ V /| \__ \ | (_) | | | | | | | | (_| |
| .__/|_|  \___/ \_/ |_|___/_|\___/|_| |_|_|_| |_|\__, |
|_|                                               |___/ 
</pre>

## bigip-provisioning 
Ansible role to automate provisioning tasks on a BIG-IP. 
The role will perform the following
* Configure VLANs                        (tags: vlans)
* Configure Self-IPs                     (tags: selfips)
* Create nodes (with health monitors)    (tags: nodes)
* Create pool                            (tags: pool)
* Create SNAT pool                       (tags: snatpool)
* Assign members to pool and SNAT pool   (tags: addtopool)
* Create a HTTPS virtual server          (tags: virtualserver)

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
