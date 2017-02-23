Session 3
Assignment 3

The main components of Hadoop 2.x are:
•	HDFS
•	YARN
•	MapReduce
          
1)	HDFS:
There are two major categories of HDFS namely,
  HIGH AVAILABILITY:
      In Hadoop 1.x, the NameNode was a single point of failure (SPOF) in an HDFS cluster. Each cluster had a single NameNode, and if that machine or process became unavailable, the cluster as a whole would be unavailable.
      But in a typical HA cluster of Hadoop 2.x, two separate machines are configured as NameNodes. At any point in time, exactly one of the NameNodes is in an Active state, and the other is in a Standby state. The Active NameNode is responsible for all client operations in the cluster, while the Standby simply acts as a slave, maintaining enough state to provide a fast failover if necessary.

        1) Hadoop 2.x supports two Name Nodes at a time one node is active and another is standby namenode
        2) Active Name Node handles the client operations in the cluster
        3) Standby Name Node manages metadata same as Secondary Name Node in Hadoop 1.x
        4) When Active Name Node is down, Standby Name Node takes over and will handle the client operations then after
        5) HDFS HA can be configured by two ways
  i.	Using Shared NFS Directory
  ii.	Using Quorum Journal Manager
  HDFS FEDERATION:
•	Hadoop 2.x Architecture which allows to manage multiple namespaces by enabling multiple Name Nodes. So on HDFS shell you have multiple directories available but it may be possible that two different directories are managed by two active Name Nodes at a time.
•	HDFS consists of a number of daemons namely,
                  1) Master Daemon --Name Node.
                  2) Slave Daemon --Data Node.
                  3) Backup Daemon --Secondary Name Node
                  
1)	Name Node:
	Name node is usually 1 in number.
	It runs on a high end admin machine.

2)	Data Node:
	Data node is usually many in number.
	It usually runs on commodity machines.
	For every 3 minutes it sends a trigger to name node to inform that it is alive.

3)	Secondary Name Node:
	It is also usually 1 in number.
	The main function is to back up the Meta data stored by Master Daemon.
	It connects to master daemon every hour.
	If primary name node crashes, secondary name node comes into play.
    
2)	YARN:
	YARN stands for Yet Another Resource Negotiator.
	It is new Component in Hadoop 2.x Architecture.
	YARN combines a central resource manager that reconciles the way applications use Hadoop system resources with node manager agents that monitor the processing operations of individual cluster nodes. 
	Running on commodity hardware clusters, Hadoop has attracted particular interest as a staging area and data store for large volumes of structured and unstructured data intended for use in analytics applications.
	Separating HDFS from MapReduce with YARN makes the Hadoop environment more suitable for operational applications that can't wait for batch jobs to finish.
 
3)	MAP REDUCE:
	MapReduce has replace old daemon process Job Tracker and Task Tracker with the components of YARN Resource Manager and Node Manager respectively. 
	These two components are responsible for executing distributed data computation jobs in Hadoop 2.x.
       
	Resource Manager:
	This is usually 1 in number.
	It usually runs on a high end machine (similar as NameNode in Hadoop 1.x).
	This daemon process runs on master node (may run on the same machine as name node for smaller clusters).
	It is responsible for getting job submitted from client and schedule it on cluster, monitoring running jobs on cluster and allocating proper resources on the slave node.
	It communicates with Node Manager Daemon process on the slave node to track the resource utilization.
	It uses two other processes named Application Manager and Scheduler for MapReduce task and resource management.

	Node Manager:
	It can be many in number.
	It runs on a lot of commodity machines (low end machines).
	This daemon process runs on slave nodes (normally on HDFS Data node machines).
	It is responsible for coordinating with Resource Manager for task scheduling and tracking the resource utilization on the slave node.
	It uses other daemon process like Application Master and Container for MapReduce task scheduling and execution on the slave node.
