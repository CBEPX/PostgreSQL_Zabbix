# Monitoring PostgreSQL in Zabbix 3.2

PostgreSQL is a modern, dynamically developing database management system with a very large set of capabilities that allow you to solve a wide range of tasks. The use of PostgreSQL generally refers to a very critical segment of the IT infrastructure that is associated with processing and storing data. Given the special place of the Data Base in the infrastructure and the degree of criticality of the tasks assigned to it, the question arises of monitoring and proper control over the operation of the DBMS. In this regard, PostgreSQL has extensive internal means of collecting and storing statistics. Collected statistics allows you to get a fairly detailed picture of what happens under the hood during the operation of the DBMS. This statistics is stored in special system tables-views and is constantly updated. Performing ordinary SQL queries in these tables, you can get a variety of data on databases, tables, indexes and other subsystems of the DBMS.
Below I describe the way and means for monitoring PostgreSQL in the Zabbix monitoring system. I like this monitoring system because it provides ample opportunities for realizing the most customary monitoring of various systems and processes.

Monitoring will be based on SQL queries to the statistics tables. The queries themselves are configured as an additional configuration file to the zabbix agent, in which the SQL queries are wrapped in the so-called. UserParameters - user-defined monitoring parameters. The custom parameter in Zabbix is ​​a great way to configure monitoring for non-standard things, such things in our case will be the parameters of PostgreSQL. Each user parameter consists of two elements: Key name and Command. The key name is a unique name that does not intersect with other key names. The command is the actual action command that the zabbix agent must execute. In the expanded version, this command can be passed various parameters.


# Install 

Install the zabbix-agent  and add user parametr in etc/zabbix/zabbix_agentd.conf

after restart zabbix agent 


```bash
 systemctl restart zabbix-agent
 ```

Let's give the user access to the database

```bash
 /var/lib/pgsql/9.4/data/pg_hba.conf
 
host    all             postgres             127.0.0.1/32            trust
 ```

and restart for apply 


```bash
service postgresql-9.4 restart
 ```

Cheсk the connect to Data Base 

```bash
 sudo -u postgres psql -h 127.0.0.1 -p 5432 -U postgres -d freeswitchdb
 ```
 
 
 # Import template in Zabbix Server 
 
 Then we import the template and add it to the network node, after that go to the macro and set access to the database
 
 ![alt text](https://github.com/SKletsov/PostgreSQL_Zabbix/blob/master/zabbix.PNG)
 
 also you can import complex screen 
 
 ![alt text](https://raw.githubusercontent.com/SKletsov/PostgreSQL_Zabbix/master/complex.PNG)

 
 
 
 
 
 
