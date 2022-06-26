
### Challenge 01 

A 3-tier environment is a common setup. Use a tool of your choosing/familiarity create these
resources. Please remember we will not be judged on the outcome but more focusing on the
approach, style and reproducibility.

##### Solution

Entire solution is bundled into ansible folder. The folder can be downloaded and run with below instruction 

**File hierarchy**

```
ansible
│   ├── ansible.cfg
│   ├── inventories
│   │   └── hosts
│   └── playbooks
│       ├── applserver
│       │   └── applserver.yaml
│       ├── database
│       │   ├── dbserver.yaml
│       │   ├── files
│       │   └── vars
│       │       └── cred.yaml
│       └── webserver
│           ├── files
│           │   └── apache2.conf-2.4.52
│           ├── handlers
│           │   └── main.yml
│           ├── vars
│           │   └── default.yaml
│           └── webserver.yaml
```

Files with the name **cred.yaml** contain passwords and hence encrypted with `ansible vault`

**Assumptions**

- Webserver, Application server and Database to be installed on 3 different machines.
- Files contain all custom configurations files
- Credentials and secrets to be stored in separate file cred.yaml vars directory. Cred.yaml is encrypted with vault password to ensure data protection.
- default configuration parameter to be stored in separate file default.yaml in var direcory
- handler folder have all custom handler defined
- No ansible role has been used in this solution as it felt not needed for this example.




**export ansible and test connection**

```
cd challenge01/ansible

export ANSIBLE_CONFIG=$(pwd)/ansible.cfg
ansible all -m ping 

ansible-vault encrypt ansible/playbooks/database/vars/cred.yaml
```

**Run playbook to set up 3 tier architecture**

```
ansible-playbook playbooks/webserver/apache2.yaml
ansible-playbook playbooks/database/mysql.yaml --ask-vault-pass
ansible-playbook playbooks/applserver/tomacat.yaml  - WIP
```