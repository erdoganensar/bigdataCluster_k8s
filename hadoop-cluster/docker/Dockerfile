FROM ensaradaletai/bigdata_baseimg

WORKDIR /root

ENV VERSION={hadoop-version} \
    ZOOKEEPER_VERSION={zookeeper-version} \
    SPARK_VERSION={spark-version} \
    SCALA_VERSION={scala-version} \
    HIVE_VERSION={hive-version} \
    ZOOKEEPER_HOME=/usr/local/apache-zookeeper-{zookeeper-version}-bin \
    HADOOP_HOME=/usr/local/hadoop-{hadoop-version} \
    SPARK_HOME=/usr/local/spark-{spark-version}-bin-hadoop3 \
    HIVE_HOME=/usr/local/apache-hive-{hive-version}-bin


ADD hadoop-$VERSION.tar.gz apache-zookeeper-$ZOOKEEPER_VERSION-bin.tar.gz spark-$SPARK_VERSION-bin-hadoop3.tgz apache-hive-$HIVE_VERSION-bin.tar.gz /usr/local/

ENV HADOOP_CONF_DIR=$HADOOP_HOME/etc/hadoop \
    HADOOP_MAPRED_HOME=$HADOOP_HOME \
    HADOOP_COMMON_HOME=$HADOOP_HOME \
    YARN_CONF_DIR=$HADOOP_HOME/etc/hadoop \
    PYTHONHASHSEED=1 \
    PYSPARK_PYTHON=python3 \
    SPARK_CONF_DIR=$SPARK_HOME/conf \
    HIVE_CONF_DIR=$HIVE_HOME/conf \
    ZOOBINDIR=$ZOOKEEPER_HOME/bin \
    ZOO_LOG_DIR=$ZOOKEEPER_HOME/logs \
    IJAVA_CLASSPATH=$SPARK_HOME/jars/* \
    PATH=$PATH:$HADOOP_HOME/bin:$HADOOP_HOME/sbin:$ZOOKEEPER_HOME/bin:$SPARK_HOME/bin:$SPARK_HOME/sbin:$HIVE_HOME/bin

COPY config/hadoop/* config/zookeeper/* config/spark/* config/hive/* config/db/* /tmp/

RUN mkdir -p $HADOOP_HOME/logs /root/.ssh $HIVE_HOME/tmp /opt $ZOOKEEPER_HOME/logs && \
    mv /tmp/ssh_config /root/.ssh/config && \
    mv /tmp/hadoop-env.sh $HADOOP_HOME/etc/hadoop/hadoop-env.sh && \
    cp /tmp/hdfs-site.xml $HADOOP_HOME/etc/hadoop/hdfs-site.xml && \ 
    cp /tmp/core-site.xml $HADOOP_HOME/etc/hadoop/core-site.xml && \
    mv /tmp/mapred-site.xml $HADOOP_HOME/etc/hadoop/mapred-site.xml && \
    mv /tmp/yarn-site.xml $HADOOP_HOME/etc/hadoop/yarn-site.xml && \
    mv /tmp/capacity-scheduler.xml $HADOOP_HOME/etc/hadoop/capacity-scheduler.xml && \
    mv /tmp/spark-env.sh $SPARK_HOME/conf/spark-env.sh && \
    cp /tmp/hive-site.xml $SPARK_HOME/conf/hive-site.xml && \
    mv /tmp/core-site.xml $SPARK_HOME/conf/core-site.xml && \
    mv /tmp/hdfs-site.xml $SPARK_HOME/conf/hdfs-site.xml && \
    mv /tmp/hive-site.xml $HIVE_HOME/conf/hive-site.xml && \
    ln -s /tmp/postgresql-42.7.0.jar $HIVE_HOME/lib/postgresql-42.7.0.jar && \
    ln -s /tmp/postgresql-42.7.0.jar $SPARK_HOME/jars/postgresql-42.7.0.jar && \
    ln -s /tmp/iceberg-spark-{spark-version}.12-1.4.2.jar $SPARK_HOME/jars/iceberg-spark-{spark-version}.12-1.4.2.jar && \
    chmod +x /tmp/start-master-hadoop.sh && \
    chmod +x /tmp/check-slave-status.sh && \
    chmod +x /tmp/start-worker-hadoop.sh && \
    chmod +x /tmp/init-cluster-config.sh && \
    chmod +x /tmp/add-host-info.sh && \
    chmod +x $HADOOP_HOME/sbin/start-dfs.sh && \
    chmod +x $HADOOP_HOME/sbin/start-yarn.sh && \
    chmod +x $HADOOP_HOME/sbin/yarn-daemon.sh
