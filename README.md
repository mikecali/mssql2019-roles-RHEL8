## MSSQL ROLE

This is a forked from https://github.com/kyleabenson/ansible-role-mssql
I have added some improvements and here is the results.

# To Install and configure MSSQL either in RHEL 8 on CentOS 8 follow the steps below:

1. Clone this repository
2. Run the playbook: 

          $ ansible-playbook site.yaml -e @vars.yaml -vvv

3. Verify the installation
         
          $ systemctl status mssql-server
         
4. Check the version of the installed SQL Server
           
          $ sqlcmd -S localhost -U SA -P 'P@ssWORD!'
           
          >> SELECT @@version
          >> GO

5. Verify or list the DB created by the playbook
            
          >> EXEC sp_databases
          >> GO

# To delete the installation

1. Run this playbook:
          
          ansible-playbook site.yaml -e @vars.yaml -vvv

2. Done
