FROM java:8

ENV ENABLE_INIT_DAEMON true
ENV INIT_DAEMON_BASE_URI http://identifier/init-daemon
ENV INIT_DAEMON_STEP spark_master_init

ENV SPARK_VERSION=2.3.1
ENV HADOOP_VERSION=2.7

RUN wget https://archive.apache.org/dist/spark/spark-${SPARK_VERSION}/spark-${SPARK_VERSION}-bin-hadoop${HADOOP_VERSION}.tgz
RUN tar -xvzf spark-${SPARK_VERSION}-bin-hadoop${HADOOP_VERSION}.tgz
RUN mv spark-${SPARK_VERSION}-bin-hadoop${HADOOP_VERSION} spark
RUN rm spark-${SPARK_VERSION}-bin-hadoop${HADOOP_VERSION}.tgz
      
RUN apt-get update
RUN apt-get install -y python3 python3-setuptools python3-pip


# Fix the value of PYTHONHASHSEED
# Note: this is needed when you use Python 3.3 or greater
ENV PYTHONHASHSEED 1

RUN apt-get install -y net-tools

RUN wget https://repo.anaconda.com/archive/Anaconda3-5.2.0-Linux-x86_64.sh
RUN chmod +x Anaconda3-5.2.0-Linux-x86_64.sh
RUN ./Anaconda3-5.2.0-Linux-x86_64.sh -b -p /opt/conda

RUN apt-get install -y vim
RUN ln -s /opt/conda/bin/python3.6 /usr/bin/python3.6.5
RUN echo "export PYSPARK_PYTHON=/opt/conda/bin/python3.6" >> /spark/bin/load-spark-env.sh
RUN echo "export PYSPARK_DRIVER_PYTHON=python3.6.5" >> /spark/bin/load-spark-env.sh


#NEED TWO TIMES
RUN apt-get -y autoremove python --purge
RUN apt-get -y autoremove python --purge
RUN ln -s /opt/conda/bin/python3.6 /usr/bin/python


ENV NB_UID=1000
ENV NB_GID=100 
ENV NB_USER=spark
RUN useradd -m -s /bin/bash -N -u $NB_UID $NB_USER
RUN usermod -aG sudo $NB_USER
USER $NB_UID

COPY master.sh /

ENV SPARK_MASTER_PORT 7077
ENV SPARK_MASTER_WEBUI_PORT 8080
ENV SPARK_MASTER_LOG /spark/logs
EXPOSE 8080 7077 6066
CMD ["/bin/bash", "/master.sh"]

#COPY worker.sh /

#ENV SPARK_WORKER_WEBUI_PORT 8081
#ENV SPARK_WORKER_LOG /spark/logs
#ENV SPARK_MASTER "spark://spark-master:7077"
#EXPOSE 8081
#CMD ["/bin/bash", "/worker.sh"]

