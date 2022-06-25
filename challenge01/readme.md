
Challenge 01

**A 3-tier environment is a common setup. Use a tool of your choosing/familiarity create these
resources. Please remember we will not be judged on the outcome but more focusing on the
approach, style and reproducibility.**

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


