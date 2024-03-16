### UCSX-IMM-Ansible

Ansible playbooks for Build a Intersight Managed UCSX along with service profiles
-------------



**Summary :** These are a group of playbooks for Day 0 build for a Cisco UCSX till creation of service profiles. Day 0 Cisco UCSX involves multiple policy , pool creation which need to be automated. With Service profile templates , Day 1 activities will be very easy.  I found multiple references for UCSX deployment and they are part of bigger deployment hence sometime confusing . These playbooks are clean and for deploy UCSX related only. It uses Ansibles roles to stucture the codes. It also covers multiple scenarions for deploying service profiles

-----



References :

https://github.com/ucs-compute-solutions
, https://github.com/CiscoDevNet/intersight-ansible

-----------------
## Ansible preparation and Intersight API 

Install Intersight Ansible

Prior to installing Intersight Ansible, make sure that you have already installed Ansible on your administration host, then install Intersight Ansible by typing the following:

[root@###### ~]# ansible-galaxy collection install cisco.intersight

Process install dependency map

Starting collection install process

Installing 'cisco.intersight:1.0.18' to '/root/.ansible/collections/ansible_collections/cisco/intersight'

To run the Intersight playbooks, add the following variable in the defaults section of /etc/ansible/ansible.cfg:

[defaults]

jinja2_native = True

This option preserves variable types like VLAN numbers during template operations.

Procedure 1.      Generate Intersight API Keys

Note:     To start using the provider the API Key, Secret Key, and Intersight endpoint URL are required.

Step 1.     Log into Cisco Intersight.

Step 2.     Go to Settings, API Keys and click on Generate API Keys.

Step 3.     Enter a description and click Generate

Now Copy this ID and content of the kep to a file mentioned in ansible variable


**Setting up Variables All the variables used in this framework are defined in the following locations:**
-----------------



1. Variable that require customer inputs are part of group_vars/. Update API key on inventory and ucs.yml (two location) 
2. Variable that do not typically require customer input (e.g. descriptions etc.) are present under role_name/defauls/main.yml.

**Playbook Execution Commands**
-----------------
Setup domain profile : (Pre-create port policy and QoS policy). This playbook use some variables from inventory file which can be easily moved to group variable. 

ansible-playbook Create_domain_profile.yml -i inventory

1. Setup Pools in Intersight: ansible-playbook create_UCSX_pools.yml 
2. Setup Policies in Intersight: ansible-playbook Create_UCSX_Server_Policies.yml 
3. Setup Server Profile Template(s) in Intersight: ansible-playbook Create_UCSX_Server_Profile_Templates.yml



**Server profiles**

There may be multiple scenarios for deploying server profiles 

1) Derive profiles from template and then deploy 

ansible-playbook Derive_UCSX_Service_Profile.yml 

2) create profiles along with assigneing them to individual servers
   
  Step1 :  run  gather_moid_servers.yml to collect the MOID's in a temp file 
  
        ansible-playbook gather_moid_servers.yml -i ../inventory   # it will collect the MOID of the servers ( I am using devnet lab here ) and create a file /tmp/inventory_server_moid.yml
  
  Step2 : run create_server_profiles.yml to create required number of profiles
    
    ansible-playbook create_server_profiles.yml -i ../inventory
