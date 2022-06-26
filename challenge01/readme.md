

### Challenge 01 

A 3-tier environment is a common setup. Use a tool of your choosing/familiarity create these
resources. 

##### Solution

Entire solution is bundled into ansible folder. The folder can be downloaded and run with below instruction 

**File hierarchy**

```
ansible
├── ansible.cfg
├── inventories
│   └── hosts
└── playbooks
    ├── applserver
    │   ├── binaries
    │   │   └── apache-tomcat-10.0.22.tar.gz
    │   ├── files
    │   │   └── tomcat.service
    │   └── tomcat.yaml
    ├── database
    │   ├── files
    │   ├── mysql.yaml
    │   └── vars
    │       └── cred.yaml
    └── webserver
        ├── apache2.yaml
        ├── files
        │   └── apache2.conf-2.4.52
        ├── handlers
        │   └── main.yml
        └── vars
            └── default.yaml
```

Files with the name **cred.yaml** contain passwords and hence encrypted with `ansible vault`

**Assumptions**

- Webserver, Application server and Database to be installed on 3 different machines.
- Files contain all custom configurations files.
- Credentials and secrets to be stored in separate file cred.yaml in the vars directory. cred.yaml is encrypted with vault password to ensure data protection.
- Default configuration parameter to be stored in separate file default.yaml in var direcory
- Handler folder have all custom handler defined
- No ansible role has been used in this solution as felt not needed for this example.




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
ansible-playbook playbooks/applserver/tomcat.yaml
```
