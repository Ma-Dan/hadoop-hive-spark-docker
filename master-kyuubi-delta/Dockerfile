FROM hadoop-hive-spark-base

ARG USERNAME=jupyter
ARG GROUPNAME=jupyter
USER root
RUN mkdir -p /opt/apache-kyuubi-1.9.0-bin && chown -R $USERNAME:$GROUPNAME /opt/apache-kyuubi-1.9.0-bin

USER $USERNAME

ENV NAMEDIR=/opt/hadoop/dfs/name
RUN mkdir -p /opt/hadoop/dfs/name
VOLUME /opt/hadoop/dfs/name

#ENV NAMESECONDDIR=/opt/hadoop/dfs/namesecondary
#RUN mkdir -p /opt/hadoop/dfs/namesecondary
#VOLUME /opt/hadoop/dfs/namesecondary

ENV SPARK_PUBLIC_DNS=localhost
ENV SPARK_LOGS_HDFS_PATH=/var/log/spark
ENV SPARK_JARS_HDFS_PATH=/spark/jars

#Kyuubi & delta
COPY apache-kyuubi-1.9.0-bin.tgz /opt/apache-kyuubi-1.9.0-bin.tgz
RUN tar -xf /opt/apache-kyuubi-1.9.0-bin.tgz -C /opt/apache-kyuubi-1.9.0-bin --strip-components 1 && sudo rm /opt/apache-kyuubi-1.9.0-bin.tgz
COPY delta-core_2.12-2.3.0.jar /opt/spark/jars
COPY delta-storage-2.3.0.jar /opt/spark/jars
COPY kyuubi-defaults.conf /opt/apache-kyuubi-1.9.0-bin/conf
COPY kyuubi-env.sh /opt/apache-kyuubi-1.9.0-bin/conf

COPY run.sh /usr/local/sbin/run.sh
RUN sudo chmod a+x /usr/local/sbin/run.sh
CMD ["run.sh"]