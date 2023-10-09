# action step Task 1 + Task 2
# Task 1
# Migrate data from other cloud or on promise database to Huawei Cloud using CDM
```
Create/buy new pruducts
```

```
1. Buy new ECS: 
In the navigation pane, choose ECS(Elastic Cloud Server) and buy new ECS. 
The Region select Bangkok
For billing Mode you need select Pay-per-use
For Specifications choose 2vCUPs 4GiB
In Image, you need select Public Image, Ubuntu, Ubuntu 22.04.
You need set your own password 
```
```
2. Buy new CDM:
In the navigation pane, choose CDM(Cloud Data Migration) 
open the Cluster management. 
If you don’t have your own CDM, please buy new cluster.
```

```
3. Buy new DWS and OBS:
In the navigation pane, choose DWS and OBS, and buy new DWS and OBS
```
```
Create function and links
```
```
1. Enable the SFTP function in the Ubuntu system(two methods).
(1)In MobaXterm open the Session, select SFTP
Enter "Public IP address" in Remote host and enter "root" in Username. 
(2)You can using command line to enable the SFTP function
Refer to this document: https://tecadmin.net/setup-sftp-server-on-ubuntu/
```
```
2. Connect using your own key and SSH client: 
Download the MobaXterm at this: https://mobaxterm.mobatek.net/
Open the MobaXterm and enter this: ssh root@{$your_ip_address}
```
```
3. Using the SFTP function connect ECS and CDM
Open the job management and create link, choose SFTP
```
```
4. Connect CDM and OBS, in CDM choose job management
Create link to OBS, the type is OBS connector 
Establish the link and test connectivity
After that, choose Table/File Migration, and create job, 
Choose the source configuration and destination job configuration, test connectivity
```
```
5. Create link between CDM and DWS and the type is JDBC connector. 
Table/File Migration to create a new job, 
Choose the source configuration and destination job configuration, test connectivity
```
# Task 2
# Read data from OBS to DWS
```
Read data from OBS to DWS
```
```
Download Dbeaver at this: https://dbeaver.io/
Enter the Host, get it from dws
Database: postgres
Enter the Username and Password, test connectivity
```
```
You can use the following code as a practical example.
```
```
#create Foreign Table
DROP FOREIGN TABLE name_list;

CREATE FOREIGN TABLE name_list
(
    id                integer        not null,
    full_name                   char(128)       not null,
    first_name                 char(128)           ,
    last_name                char(128)                         
) 
SERVER gsmpp_server 
OPTIONS(
LOCATION 'obs://yufeigao/root1/gyf.csv',
FORMAT 'CSV' ,
DELIMITER ',',
encoding 'utf8',
header 'false',
ACCESS_KEY '5BMZCKQ61TUZR90GFPGA',
SECRET_ACCESS_KEY 'aJIXIMat8VxtwcBrCZOFUJs8V9lcJAhk8ywXchGW',
fill_missing_fields 'true',
ignore_extra_data 'true'
);
READ ONLY 
LOG INTO name_info 
```
```
#Create Inner Table
DROP TABLE IF EXISTS inner_name_list;
CREATE TABLE inner_name_list
( 
id                integer        not null,
    full_name                   char(128)       not null,
    first_name                 char(128)           ,
    last_name                char(128)
)
WITH (orientation = column, COMPRESSION = MIDDLE)
DISTRIBUTE BY HASH(id);
```

```
# Data Migration
INSERT INTO gaoyufei.inner_name_list 
SELECT * FROM gaoyufei.name_list 
```
```
#Test the task if is successful
select *from gaoyufei.inner_name_list inl 
```




