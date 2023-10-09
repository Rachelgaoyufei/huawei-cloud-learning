# action step
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

