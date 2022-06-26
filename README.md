

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



### Challenge 02

We need to write code that will query the meta data of an instance within AWS and provide a
json formatted output.

##### Solution

Haven't have worked with AWS, however in Azure to retrieve metadata they have `Azure Instance Metadata Service`
which  provides virtual machine instances.

Login into the vm and run the below curl command - output is in JSON

With jq command we can loop thru the values and retive only those required.

```
curl -s -H Metadata:true --noproxy "*" "http://169.254.169.254/metadata/instance?api-version=2021-02-01" | jq
```

### Challenge 03

We have a nested object, we would like a function that you pass in the object and a key and get
back the value. How this is implemented is up to you.

Example Inputs

object = {“a”:{“b”:{“c”:”d”}}}

key = a/b/c

object = {“x”:{“y”:{“z”:”a”}}}

key = x/y/z

value = a

##### Solution

json_search_func -> file contains the function to retreive given key from json object

**testing**

Switch to the script directory and source the script file

```
cd challenge03/
source json_search_func
```

test outcome

```
root@MSI# object='{"x":{"y":{"z":"a"}},"p":"b","c":"ui"}'
root@MSI# key='"y"'
root@MSI#
root@MSI# searchkeyval $object $key
"y" -> {"z":"a"}


root@MSI# object='{"x":{"y":{"z":"a"}},"p":"b","c":"ui"}'
root@MSI# key='"c"'
root@MSI#
root@MSI# searchkeyval $object $key
"c" -> "ui"

```