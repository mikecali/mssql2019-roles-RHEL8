# MSSQL ROLE To Deploy MSSQL19 on RHEL 8/CentOS 8

This is a forked from https://github.com/kyleabenson/ansible-role-mssql, I have added some improvements and here is the results.

## Requirements:

No special requirements; note that this role requires root access, so either run it in a playbook with a global become: yes, or invoke the role in your playbook like:

      - hosts: localhost
        become: yes
        roles:
          - pre-reqs
          - ansible-role-mssql
        tasks:
        - name: Wait up to 60 seconds for server to become available after creation
          wait_for:
            port: 1433
            timeout: 60
        - name: Create new db
          include_role:
          name: ansible-role-mssql
          tasks_from: new_db

This repository has ansible.cfg that I uploaded so you can simply run the playbook after cloning.
Note that this repo contains 2 roles:
          
          pre-reqs
          ansible-role-mssql

# To Install and configure MSSQL either in RHEL 8 on CentOS 8 follow the steps below:

1. Clone this repository


2. Run the playbook: 

          $ ansible-playbook site.yaml -e @vars.yaml -vvv

3. Verify the installation
         
          $ systemctl status mssql-server
         
4. Check the version of the installed SQL Server
           
          $ sqlcmd -S localhost -U SA -P 'P@ssWORD!'
           
          1> SELECT @@version
          2> GO
 
          -------------------------------------------------------------------------------------------------------------------------------------------------------- 
         Microsoft SQL Server 2019 (RTM-CU8) (KB4577194) - 15.0.4073.23 (X64) 
	   Sep 23 2020 16:03:08 
	   Copyright (C) 2019 Microsoft Corporation
	   Enterprise Evaluation Edition (64-bit) on Linux (Red Hat Enterprise Linux 8.2 (Ootpa)) <X64>                                                                        

        (1 rows affected)


5. Verify or list the DB created by the playbook
            
          1> EXEC sp_databases
          2> GO

# To delete the installation

1. Run this playbook:
          
          $ ansible-playbook site.yaml -e @vars.yaml -vvv

2. Done
