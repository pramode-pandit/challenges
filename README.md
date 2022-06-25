

### Challenge 01 

A 3-tier environment is a common setup. Use a tool of your choosing/familiarity create these
resources. Please remember we will not be judged on the outcome but more focusing on the
approach, style and reproducibility.

**Solution**

Switch to ansible solution directory

```
cd challenge01/ansible
```


export ansible and test connection

```
export ANSIBLE_CONFIG=$(pwd)/ansible.cfg
ansible all -m ping 
```

Run playbook to set up 3 tier architecture

```
ansible-playbook playbooks/webserver/apache2.yaml
ansible-playbook playbooks/applserver/tomacat.yaml
ansible-playbook playbooks/database/mysql.yaml
```

### Challenge 02

We need to write code that will query the meta data of an instance within AWS and provide a
json formatted output.

### Challenge 03

We have a nested object, we would like a function that you pass in the object and a key and get
back the value. How this is implemented is up to you.
Example Inputs
object = {“a”:{“b”:{“c”:”d”}}}
key = a/b/c
object = {“x”:{“y”:{“z”:”a”}}}
key = x/y/z
value = a

**Solution**

```
cd challenge03

source searchscript

object='{"x":{"y":{"z":"a"}},"p":"b"}'
key='"y"'

# execute script function to search key value

searchkeyval $object $key
```