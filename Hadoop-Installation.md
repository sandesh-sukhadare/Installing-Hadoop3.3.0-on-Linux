# Installing Hadoop on Linux (Ubuntu)

### Update apt repo
  ```
  sudo apt get update
  ```

### Install OpenJDK
  ```
  sudo apt install openjdk-8-jdk -y
  ```
### Install OpenSSH
  ```
  sudo apt install openssh-server openssh-client -y
  ```
### Enable passwordless SSH for the user
  ```
  ssh-keygen -t rsa -P '' -f ~/.ssh/id_rsa
  ```
### Store the public key as authorized_keys in the ssh directory
  ```
  cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys
  ```
### Set the permission for your user
  ```
  chmod 0600 ~/.ssh/authorized_keys
  ```
### SSH to localhost
  ```
  ssh localhost
  ```
### Create a directory for all hadoop 
  ``` 
  cd ~
  mkdir Ecosystem
  cd Ecosystem
  ```
### Download hadoop tar file
  ```
  wget https://archive.apache.org/dist/hadoop/common/hadoop-3.3.0/hadoop-3.3.0.tar.gz
  ```
### Extract tar file
  ``` 
  tar xzf hadoop-3.3.0.tar.gz
  ```
### Create folders for namenode and datanode
  ```
  cd hadoop-3.3.0/
  mkdir -p data/namenode
  mkdir -p data/datanode
  ```
### Edit .bashrc file
  ```
  nano ~/.bashrc
  ```
  Add your username in HADOOP_HOME path
  ```
  #java
  export JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64
  
  #Hadoop Related Options
  export HADOOP_HOME=/home/"your_username"/Ecosystem/hadoop-3.3.0
  export HADOOP_INSTALL=$HADOOP_HOME
  export HADOOP_MAPRED_HOME=$HADOOP_HOME
  export HADOOP_COMMON_HOME=$HADOOP_HOME
  export HADOOP_HDFS_HOME=$HADOOP_HOME
  export YARN_HOME=$HADOOP_HOME
  export HADOOP_COMMON_LIB_NATIVE_DIR=$HADOOP_HOME/lib/native
  export PATH=$PATH:$HADOOP_HOME/sbin:$HADOOP_HOME/bin
  export HADOOP_OPTS="-Djava.library.path=$HADOOP_HOME/lib/native"
  ```
## Configure hadoop files
  ``` 
  cd ~/Ecosystem/hadoop-3.3.0/etc/hadoop/

  ```
  ### 1. hadoop-env.sh
  ```
  nano hadoop-env.sh
  ```
  Uncomment JAVA_HOME by removing # and modify it to (line 37)
  ```
  JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64
  ```
  ### 2. core-site.xml
  ```
  nano core-site.xml
  ```
  paste the following code inside configuration<>
  ```
  <property>
  <name>fs.default.name</name>
  <value>hdfs://localhost:9000</value>
  </property>
  ```
  ### 3. hdfs-site.xml
  ```
  nano hdfs-site.xml
  ```
  Insert your username at line 7 & 11
  ```
  <property>
  <name>dfs.replication</name>
  <value>1</value>
  </property>
  <property>
  <name>dfs.namenode.name.dir</name>
  <value>/home/"your_username"/Ecosystem/hadoop-3.3.0/data/namenode</value>
  </property>
  <property>
  <name>dfs.datanode.data.dir</name>
  <value>/home/"your_username"/Ecosystem/hadoop-3.3.0/data/datanode</value>
  </property>
  ```
### 4. mapred-site-xml
  ```
  nano mapred-site.xml
  ```
  ```
  <property> 
  <name>mapreduce.framework.name</name> 
  <value>yarn</value> 
  </property>
  ```
### 5. yarn-site.xml
  ```
  nano yarn-site.xml
  ```
  ```
  <property>
  <name>yarn.nodemanager.aux-services</name>
  <value>mapreduce_shuffle</value>
  </property>
  <property>
  <name>yarn.nodemanager.aux-services.mapreduce.shuffle.class</name>
  <value>org.apache.hadoop.mapred.ShuffleHandler</value>
  </property>
  <property>
  <name>yarn.resourcemanager.hostname</name>
  <value>127.0.0.1</value>
  </property>
  <property>
  <name>yarn.acl.enable</name>
  <value>0</value>
  </property>
  <property>
  <name>yarn.nodemanager.env-whitelist</name>   
  <value>JAVA_HOME,HADOOP_COMMON_HOME,HADOOP_HDFS_HOME,HADOOP_CONF_DIR,CLASSPATH_PERPEND_DISTCACHE,HADOOP_YARN_HOME,HADOOP_MAPRED_HOME</value>
  </property>
  ```
### Format HDFS NameNode
  ```
  hdfs namenode -format
  ```
### Start Hadoop Cluster
  ```
  start-all.sh
  ```
### Check running processes
  ```
  jps
  ```
### Access Hadoop UI from Browser
Hadoop NameNode UI
  ```
  http://localhost:9870
  ```
YARN UI
  ```
  http://localhost:8088
  ```
  

  

  
  


  

  
  
