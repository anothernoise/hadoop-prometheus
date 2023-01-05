# hadoop-prometheus
hadoop metrics to prometheus

## Enable gathering JMX metrics

To enable JMX metrics gathering for Hadoop components, you will need to modify the configuration files for each component. Here are the steps you can follow:

Edit the `hadoop-env.sh` file and add the following lines to enable JMX monitoring:
```
export HADOOP_JMX_BASE="-Dcom.sun.management.jmxremote.ssl=false -Dcom.sun.management.jmxremote.authenticate=false"
export HADOOP_MASTER_OPTS="$HADOOP_MASTER_OPTS $HADOOP_JMX_BASE -Dcom.sun.management.jmxremote.port=10101"
export HADOOP_SLAVE_OPTS="$HADOOP_SLAVE_OPTS $HADOOP_JMX_BASE -Dcom.sun.management.jmxremote.port=10102"
```

For each Hadoop component, add the following lines to the component's configuration file (e.g. hdfs-site.xml, mapred-site.xml, etc.) to specify the JMX port:
```
<property>
  <name>hadoop.jmx.agent.port</name>
  <value>10101</value>
</property>
```
 
## Download and install the Prometheus JMX Exporter
Prometheus JMX Exporter on each node where the Hadoop component is running. You can find the latest release of the exporter here: https://github.com/prometheus/jmx_exporter/releases

Create a configuration file for the exporter, specifying the JMX endpoint of each component to be scraped. Here is an example configuration file for a DataNode:
```
---
startDelaySeconds: 15
ssl: false
lowercaseOutputName: true
lowercaseOutputLabelNames: true
whitelistObjectNames:
  - "Hadoop:service=DataNode,name=DataNodeInfo"
  - "Hadoop:service=DataNode,name=DataNodeActivity"
  - "Hadoop:service=DataNode,name=JvmMetrics"
rules:
- pattern: "Hadoop:service=DataNode,name=JvmMetrics"
  name: "hadoop_jvm_<name>"
  help: "JVM metrics for Hadoop DataNode"
  type: GAUGE
- pattern: "Hadoop:service=DataNode,name=DataNodeInfo"
  name: "hadoop_datanode_<name>"
  help: "Hadoop DataNode information"
  type: GAUGE
- pattern: "Hadoop:service=DataNode,name=DataNodeActivity"
  name: "hadoop_datanode_activity_<name>"
  help: "Hadoop DataNode activity"
  type: GAUGE

```

## Start the Prometheus JMX Exporter, 
specifying the configuration file as an argument:
this
```
./jmx_exporter -config.file=hadoop-datanode-jmx.yaml
```

Configure Prometheus to scrape the JMX Exporter endpoint for each node. You can do this by adding the following lines to the prometheus.yml configuration file:

```
  - job_name: 'hadoop-datanode'
    static_configs:
    - targets: ['<node-ip>:7071']
``` 
