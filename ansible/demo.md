# Ansible Configuration

- Since we do not have a VM environment to run ansible. We will use docker containers to simulate the environment. 

- You will set up using the docker compose yaml, 3 nodes: 1 control node, 2 remote host nodes.
- Clone this repository. 

```
cd /ansible/lab
docker compose up -d
docker exec -it <containerid_ansible> bash

// Check if ansible is installed
ansible --version 

// Check if SSH is enabled and you are able to remote into the two nodes. 
ssh root@node1

exit

ssh root@node2

exit
```

**Lab 3 - Setup the docker containers and check in the control node if Ansible is installed.**
**Lab 3 - Setup the docker containers and ssh into the remote nodes from the control node.**

```
// We can use ansible ping command to check connection to all the nodes

ansible all -m ping

// Since you dont have any inventory about nodes. We will get warning. 


// We will enable SSH Key login for both nodes
ssh-keygen -t rsa -b 2048

ssh-copy-id root@node1
ssh-copy-id root@node2

// Create a inventory list in a txt file "inventory.txt"
// Install VIM if you would like to use it.

[group1]
host1 ansible_host=node1 ansible_user=root 
host2 ansible_host=node2 ansible_user=root 

// Check if the inventory list is getting picked up 

ansible-inventory -i inventory.txt --list

// Check if you are able to connect to the other nodes

ansible all -i inventory.txt -m ping

// In the docker the default location for inventory is /etc/ansible/hosts
// Enter the invenotry list in hosts file and you do not have to use -i option with any commands

```

**Lab 3 - You should be able to connect to the hosts at this stage successfully.**

## Ansible Ad-hoc commands

- Basic Syntax

`ansible <remote_nodes> -m <module_name> -a <module_commands>`

- Check memory usage on node1

`ansible -i inventory.txt host1 -m shell -a "free -m"`

```
// Disk usage 

ansible all -i inventory.txt -m shell -a "df -h"

ansible host2 -i inventory.txt -m apt -a "name=curl state=present" -b

ansible host1 -i inventory.txt -m service -a "name=cron state=restarted" -b
```

## Create ansible hosts file

```
// Create /etc/ansible/hosts file

// Add below

node1
node2

// Check if you can connect without passing inventory

ansible all -m ping

// To view the configurations of the other nodes
ansible all -m setup

// To check uptime
ansible all -a uptime

// To create a file 
ansible all -m file -a "path=~/tmp-file state=touch"

// To delete the file
ansible all -m file -a "path=~/tmp-file state=absent"

// To list all the modules
ansible-doc -l | grep shell
```

**Lab3 - Try to create a directory uisng the ad-hoc command. PResent screenshots of the sucessful ansible run and directory in the nodes.**

## Create first playbook 

```
// Copy Create-file.yml into the control node

// Run the playbook 
ansible-playbook create-file.yml

```

**Lab 3 - Create the file playbook yml and create file in both nodes. Show using screenshot that you have successfully created the file using playbook**
- Should include response from the playbook command. 

**Lab3 - Create a new playbook to delete the file you created previously. Submit screenshots for the playbook run and screenshots that the file has been deleted from both nodes**

## Create dev group and add node 1 to it

```
// Update host file with group info
[dev]
host1 ansible_host=node1 ansible_user=root 

[test]
host2 ansible_host=node2 ansible_user=root 

// Run the playbook command for dev group only 
ansible-playbook create-file-dev.yml

```

**Lab3 - Create a new playbook for test group and demonstrate using the playbook output that you have updated only the test node**

**Lab3 - Install Nodejs using nodejs yaml. There is a issue with yaml file you need to fix it. Once installed you will get the node and npm version screenshots. Also, the successful playbook run screenshot.**

## Create Ansible role

```
// Search for roles in galaxy
ansible-galaxy role search elasticsearch --author geerlingguy

ansible-galaxy init <my_role>

ansible-galaxy install geerlingguy.postgresql

cd <folder>

ansible-playbook postgres.yaml 
```


## Conditionals

`ansible-playbook conditions.yml`
`ansible-playbook conditions-1.yml`

## Handler

`ansible-playbook handler.yml`

## Ansible Vault

```
ansible-vault create vault.yaml 

// Enter data into vault.yaml 

cat vault.yaml

ansible-vault view vault.yaml

ansible-vault edit vault.yaml

ansible-vault rekey vault.yaml
```

**Lab3 - Use the example node.yaml and clone the Lab 1 repo to both the nodes. Build the node modules** 
