# Hadoop metric Prometheus JMX exporter config




Metric name	Hadoop component	Metric location	JMX bean name	Prometheus JMX Exporter extract regular expression
namenode_status	NameNode	Service status	Hadoop:service=NameNode,name=NameNodeStatus	.*Status:(\\w+).*
namenode_capacity_used	NameNode	Storage capacity	Hadoop:service=NameNode,name=FSNamesystem	.*CapacityUsed:(\\d+).*
namenode_capacity_total	NameNode	Storage capacity	Hadoop:service=NameNode,name=FSNamesystem	.*CapacityTotal:(\\d+).*
namenode_capacity_remaining	NameNode	Storage capacity	Hadoop:service=NameNode,name=FSNamesystem	.*CapacityRemaining:(\\d+).*
hdfs_block_capacity	HDFS	Block capacity	Hadoop:service=NameNode,name=FSNamesystemState	.*BlockCapacity:(\\d+).*
hdfs_blocks_total	HDFS	Number of blocks	Hadoop:service=NameNode,name=FSNamesystemState	.*BlocksTotal:(\\d+).*
hdfs_files_total	HDFS	Number of files	Hadoop:service=NameNode,name=FSNamesystemState	.*FilesTotal:(\\d+).*
hbase_regions_total	HBase	Number of regions	Hadoop:service=HBase,name=Master,sub=Server	.*regionCount:(\\d+).*
hbase_requests_total	HBase	Number of requests	Hadoop:service=HBase,name=Master,sub=Server	.*totalRequestCount:(\\d+).*
hbase_regions_in_transition	HBase	Number of regions in transition	Hadoop:service=HBase,name=Master,sub=Server	.*regionsInTransition:(\\d+).*
mapreduce_jobs_submitted	MapReduce	Number of jobs submitted	`Hadoop:service=JobTracker,name=JobTracker	


