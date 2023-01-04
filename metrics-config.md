# Hadoop metric Prometheus JMX exporter config


## Essential Hadoop metric for monitoring
|Metric name	|Description |
|-----------|------------------|
|namenode_status	|The status of the NameNode service.|
|namenode_capacity_used	|The amount of storage capacity that is used by the NameNode, in bytes.|
|namenode_capacity_total|	The total storage capacity of the NameNode, in bytes.|
|namenode_capacity_remaining|	The amount of remaining storage capacity on the NameNode, in bytes.|
|hdfs_block_capacity|	The block capacity of the HDFS, in bytes.|
|hdfs_blocks_total|	The total number of blocks in the HDFS.|
|hdfs_files_total	|The total number of files in the HDFS.|
|hbase_regions_total|	The total number of regions in the HBase.|
|hbase_requests_total	|The total number of requests received by the HBase.|
|hbase_regions_in_transition|	The number of regions in transition in the HBase.|
|mapreduce_jobs_submitted	|The number of MapReduce jobs that have been submitted to the cluster.|
|mapreduce_jobs_completed	|The number of MapReduce jobs that have completed on the cluster.|
|mapreduce_maps_total	|The total number of map tasks that have been run on the cluster.|
|mapreduce_reduces_total	|The total number of reduce tasks that have been run on the cluster.|
|mapreduce_slots_millis_maps	|The total number of millis of map task slots that have been used on the cluster.|
|mapreduce_slots_millis_reduces|	The total number of millis of reduce task slots that have been used on the cluster.|
|yarn_apps_submitted	|The number of YARN applications that have been submitted to the cluster.|
|yarn_apps_completed|	The number of YARN applications that have completed on the cluster.|
|yarn_apps_pending|	The number of YARN applications that are pending on the cluster.|
|yarn_apps_running	|The number of YARN applications that are currently running on the cluster.|
|yarn_containers_allocated|	The total number of YARN containers that have been allocated on the cluster.|
|yarn_containers_reserved	|The total number of YARN containers that are currently reserved on the cluster.|
|yarn_containers_pending|	The total number of YARN containers that are pending on the cluster.|
|yarn_memory_allocated	|The total amount of memory that has been|


## Essential Hadoop metric for monitoring with JMX Exporter
|Metric name|	Hadoop component |	Metric desc|	JMX bean name|	Prometheus JMX Exporter template|
|-----------|------------------|-------------------------------|-----------------------------------|
|namenode_status|	NameNode	|Service status|	Hadoop:service=NameNode,name=NameNodeStatus|	.*Status:(\\w+).*|
|namenode_capacity_used |	NameNode	|Storage capacity|	Hadoop:service=NameNode,name=FSNamesystem|	.*CapacityUsed:(\\d+).*|
|namenode_capacity_total|	NameNode	|Storage capacity|	Hadoop:service=NameNode,name=FSNamesystem|	.*CapacityTotal:(\\d+).*|
|namenode_capacity_remaining|	NameNode	|Storage capacity|	Hadoop:service=NameNode,name=FSNamesystem|	.*CapacityRemaining:(\\d+).*|
|hdfs_block_capacity|	HDFS|	Block capacity|	Hadoop:service=NameNode,name=FSNamesystemState|	.*BlockCapacity:(\\d+).*|
|hdfs_blocks_total|	HDFS|	Number of blocks|	Hadoop:service=NameNode,name=FSNamesystemState|	.*BlocksTotal:(\\d+).*|
|hdfs_files_total|	HDFS	|Number of files|	Hadoop:service=NameNode,name=FSNamesystemState|	.*FilesTotal:(\\d+).*|
|hbase_regions_total|	HBase|	Number of regions|	Hadoop:service=HBase,name=Master,sub=Server|	.*regionCount:(\\d+).*|
|hbase_requests_total|	HBase|	Number of requests|	Hadoop:service=HBase,name=Master,sub=Server|	.*totalRequestCount:(\\d+).*|
|hbase_regions_in_transition|	HBase	Number of regions in transition|	Hadoop:service=HBase,name=Master,sub=Server|	.*regionsInTransition:(\\d+).*|
|mapreduce_jobs_submitted|	MapReduce|	Number of jobs submitted	|`Hadoop:service=JobTracker,name=JobTracker	| |

### Mapreduce

|Metric name|	Hadoop component	|Metric desc	|JMX bean name|	Prometheus JMX Exporter template |
|-----------|------------------|-------------------------------|-----------------------------------|
|mapreduce_jobs_submitted	|MapReduce|	Number of jobs submitted|	Hadoop:service=JobTracker,name=JobTrackerMetrics	|.*jobsSubmitted:(\\d+).*|
|mapreduce_jobs_completed|	MapReduce|	Number of jobs completed|	Hadoop:service=JobTracker,name=JobTrackerMetrics	|.*jobsCompleted:(\\d+).*|
|mapreduce_maps_total|	MapReduce	|Number of map tasks|	Hadoop:service=JobTracker,name=JobTrackerMetrics	|.*mapsTotal:(\\d+).*|
|mapreduce_reduces_total	|MapReduce|	Number of reduce tasks|	Hadoop:service=JobTracker,name=JobTrackerMetrics|	.*reducesTotal:(\\d+).*|
|mapreduce_slots_millis_maps|	MapReduce|	Millis of map task slots used|	Hadoop:service=JobTracker,name=JobTrackerMetrics	|.*slotsMillisMaps:(\\d+).*|
|mapreduce_slots_millis_reduces|	MapReduce|	Millis of reduce task slots used|	Hadoop:service=JobTracker,name=JobTrackerMetrics|	.*slotsMillisReduces:(\\d+).*|

### YARN

|Metric name|	Hadoop component|Metric location	|JMX bean name|	Prometheus JMX Exporter template|
|-----------|------------------|-------------------------------|-----------------------------------|
|yarn_apps_submitted|	YARN|	Number of applications submitted|	Hadoop:service=ResourceManager,name=RMApps|	.*AppsSubmitted:(\\d+).*|
|yarn_apps_completed|	YARN|	Number of applications completed	|Hadoop:service=ResourceManager,name=RMApps	|.*AppsCompleted:(\\d+).*|
|yarn_apps_pending|	YARN|	Number of applications pending|	Hadoop:service=ResourceManager,name=RMApps	|.*AppsPending:(\\d+).*|
|yarn_apps_running|	YARN|	Number of applications running	|Hadoop:service=ResourceManager,name=RMApps	|.*AppsRunning:(\\d+).*|
|yarn_containers_allocated	|YARN	|Number of containers allocated|	Hadoop:service=ResourceManager,name=RMActiveApplications	|.*ContainersAllocated:(\\d+).*|
|yarn_containers_reserved|	YARN|	Number of containers reserved|	Hadoop:service=ResourceManager,name=RMActiveApplications|	.*ContainersReserved:(\\d+).*|
|yarn_containers_pending|	YARN|	Number of containers pending	|Hadoop:service=ResourceManager,name=RMActiveApplications|	.*ContainersPending:(\\d+).*|
|yarn_memory_allocated|	YARN|	Amount of memory allocated, in bytes	|Hadoop:service=ResourceManager,name=RMActiveApplications	|.*MemoryAllocated:(\\d+).*|
|yarn_memory_available|	YARN	|Amount of memory available, in bytes	|Hadoop:service=ResourceManager,name=RMActiveApplications	|.*MemoryAvailable:(\\d+).*|

