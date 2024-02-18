# UCSX-IMM-Ansible
Ansible playbooks for Build a  Intersight Managed UCSX  along with service profiles 

Summery :  These are a group of playbooks for Day 0 build for a Cisco UCSX till creation of service profiles. I found multiple referecens for UCSX deployment and they are part of bigger deployment hence sometime confusing . These playbooks are clean and for deploy UCSX related only. It uses Ansibles roles to stucture the codes. It also covers multiple scenarions for deploying service profiles   

References : https://github.com/ucs-compute-solutions
             https://github.com/CiscoDevNet/intersight-ansible


Setting up Variables
All the variables used in this framework are defined in the following locations:

Variable that require customer inputs are part of group_vars/
Variable that do not typically require customer input (e.g. descriptions etc.) are present under role_name/defauls/main.yml. 

Playbook Execution Commands
Setup Pools in Intersight: ansible-playbook ./create_pools.yml -i inventory
Setup Policies in Intersight: ansible-playbook ./create_server_policies.yml -i inventory
Setup Server Profile Template(s) in Intersight: ansible-playbook ./create_server_profile_template.yml -i inventory 
