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
 
