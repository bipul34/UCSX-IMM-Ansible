### UCSX-IMM-Ansible

Ansible playbooks for Build a Intersight Managed UCSX along with service profiles
-------------



**Summery :** These are a group of playbooks for Day 0 build for a Cisco UCSX till creation of service profiles. I found multiple referecens for UCSX deployment and they are part of bigger deployment hence sometime confusing . These playbooks are clean and for deploy UCSX related only. It uses Ansibles roles to stucture the codes. It also covers multiple scenarions for deploying service profiles

-----



References :

https://github.com/ucs-compute-solutions
, https://github.com/CiscoDevNet/intersight-ansible

-----------------



**Setting up Variables All the variables used in this framework are defined in the following locations:**
-----------------



1. Variable that require customer inputs are part of group_vars/ 
2. Variable that do not typically require customer input (e.g. descriptions etc.) are present under role_name/defauls/main.yml.

**Playbook Execution Commands**
-----------------
Setup domain profile :ansible-playbook ./Create_domain_profile.yml -i inventory  (Precreate port policy and QoS policy)

1. Setup Pools in Intersight: ansible-playbook ./create_pools.yml -i inventory 
2. Setup Policies in Intersight: ansible-playbook ./create_server_policies.yml -i inventory 
3. Setup Server Profile Template(s) in Intersight: ansible-playbook ./create_server_profile_template.yml -i inventory



**Server profiles**

There may be multiple scenarios for deploying server profiles 

1) Derive profiles from template and then deploy 
ansible-playbook ./derive_profile_new.yml -i inventory

2) derive profiles adn assigned them to indivudual servers
   
  Step1 :  run  gather_moid_servers.yml to collect the MOID's in a temp file 
  
  Step2 : arrange the file in a readable list
  
  Step3 : run create_server_profiles.yml to create required number of profiles
