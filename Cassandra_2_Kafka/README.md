## PySpark Apache Kafka and  Cassandra DB 



This project demonstrates how to set up a development environment locally
This is a repo help you to understand and launch the Kafka cluster 


### Project Architecture:
![untitled (1)](https://user-images.githubusercontent.com/115451707/219657272-0b190c35-b148-43d3-a30f-7611705f3a6f.png)


## Steps to setup projects
Open Vscode
Goto Extensions
1. Install Python.
2. Dev Containers
3. Remote development
4. Cassandra's workbench
Both 2 and 3 are used to go inside the Docker container.
To start the setup
```
docker-compose -f docker-compose.yml up -d
```
Once done with the installation,
Open the workspace (the workspace path is needed for configuration to be generated), and activate the extension by running the command from the palette. Cassandra Workbench: Generate configuration. This will generate the Cassandra Workbench.jsonc configuration file.

Once done with it. Automatically, a file is added to the folder.
Switch to the Cassandra workbench panel by clicking the activity bar icon. Edit cassandraWorkbench.jsonc to suit your needs. (Configuration)
Update the username and password in the above file.


Install a few extensions in vs code to work with Cassandra db
Click on New File
Select the cluster as the password administrator from the dropdown and create the workspace.
1. Cassandra Workbench

Create a keyspace with name "ineuron"
```
CREATE KEYSPACE ineuron
	WITH REPLICATION = {
		'class': 'org.apache.cassandra.locator.SimpleStrategy',
		'replication_factor': '3'
	}
	AND DURABLE_WRITES = true;
```

Create a table Employee
```
 CREATE TABLE ineuron.EMPLOYEE(
     EMP_ID INT,
     EMP_NAME text,
     CITY text,
     STATE text,
     primary key (EMP_ID)
 );
```
To insert records into the Employee table refer to CQL_SCRIPT.cql
Once data is inserted into Cassandra.

Once the above steps are completed, execute the below command:
Write the code to read the data from Cassandra and put it into Kafka.
Click on Command Pallate and select Developers: Attach to the running container; click on that.
Select the Pyspark container, and it will open the blank Vscode.
Open a new terminal.
Follow the below commands.
ls /
cd /project
ls /
Run the producer file with the below command:
To launch the producer script
```
spark-submit --packages org.apache.spark:spark-sql-kafka-0-10_2.12:3.0.1,com.datastax.spark:spark-cassandra-connector_2.12:3.0.0  producer.py 
```
Once executed with the producer script.
open a new terminal
Follow the below commands.
ls /
cd /project
ls /
Run the consumer file with the below command:
To launch a consumer script
```
spark-submit --packages org.apache.spark:spark-sql-kafka-0-10_2.12:3.0.1 consumer.py

```
To stop the setup
```
docker-compose down
```
