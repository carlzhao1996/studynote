### Hadoop Study Note
1. [HDFS (Hadoop Distributed File System)](#hdfs)
2. [HDFS Deployment](#hdfs-deploy)

#### <div id="hdfs">HDFS (Hadoop Distributed File System)</div>
##### Usage:
1. Manage large amount of files
2. Read & Write from File system
##### Feature:
1. Distributed: Make many server as a cluster
2. CS (Client & Server) Mode
##### Master & Slave Structure:
Master: NameNode (Unique)
1. Receiving request from Client side
2. Managign all the datanode
3. Managing Metadata

Metadata-Node for data storage
1. Each file has been distributed into several pieces
2. Each file has few copies
3. Each copies storage in one of the servers

Salves: DataNode (Can be many)
1. Submitting users' request to server
2. Split files while storage
3. Merging files while reading

Secondary NameNode: Support process-Support NameNode to backup metadata

##### Storage Example:
```
500M Data Storage:
	block1:128M
	block2:128M
	block3:128M
	block4:116M

Default HDFS will duplicate each block into two pieces. Therefore each block on hdfs will exist 3 copies.

node1		node2		node3		node4
block1		block2		block3		block4
block2		block1		block2		block1
block3		block3		block4
block4
```

#### <div id="hdfs-deploy">HDFS Deployment</div>
##### Deployment Environment:
1. Local environment: Use for testing 
2. Fake distributed enviroment: one server only use for testing
3. Distributed environment: Real environment for industry

##### Linux Environment:
1. Configuring all the ip, hostname, and Mapping
2. Close Firewall or configure routing rules
3. Setup unique directory and user account
```
	sudo mkdir -p /opt/modules  ：Directory for installation
	sudo mkdir -p /opt/datas	：Directory for data storage
	sudo mkdir -p /opt/tools	：Directory for storage install package
	sudo chown -R rdedu:rdedu /opt/modules 
	sudo chown -R rdedu:rdedu /opt/datas
	sudo chown -R rdedu:rdedu /opt/tools
```
4. Setup SSH login
```
	ssh username@hostname
	exit
	ssh-keygen -t rsa
	ssh-copy-id bigdata-cdh.demo.com
```
5. Setup unique time for each server
6. Install JDK:
```
tar -zxf /opt/tools/jdk-8u91-linux-x64.tar.gz -C /opt/modules/
```
7. Configure Local Environment:
```
	sudo vim /etc/profile
	export JAVA_HOME=/opt/modules/jdk1.8.0_91
	export PATH=$PATH:$JAVA_HOME/bin
```
8. Refresh Local Enviroment
```
	source /etc/profile
```
9. Final Testing:
```
	java -version
```