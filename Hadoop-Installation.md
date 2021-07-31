# Installing Hadoop on Linux (Ubuntu)

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
  export HADOOP_HOME=/home/<"your_username">/Ecosystem/hadoop-3.3.0
  export HADOOP_INSTALL=$HADOOP_HOME
  export HADOOP_MAPRED_HOME=$HADOOP_HOME
  export HADOOP_COMMON_HOME=$HADOOP_HOME
  export HADOOP_HDFS_HOME=$HADOOP_HOME
  export YARN_HOME=$HADOOP_HOME
  export HADOOP_COMMON_LIB_NATIVE_DIR=$HADOOP_HOME/lib/native
  export PATH=$PATH:$HADOOP_HOME/sbin:$HADOOP_HOME/bin
  export HADOOP_OPTS="-Djava.library.path=$HADOOP_HOME/lib/native"
  ```
### Configure hadoop files
  ``` 
  cd ~/Ecosystem/hadoop-3.3.0/etc/hadoop/

  ```
  ## 1. hadoop-env.sh
  ```
  nano hadoop-env.sh
  ```
  Uncomment JAVA_HOME by removing # and modify it to (line 37)
  ```
  JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64
  ```
  ## 2. core-site.xml
  ```
  nano core-site.xml
  ```
  paste the following code inside "<configuration>"
  ```
  <property>
  <name>fs.default.name</name>
  <value>hdfs://localhost:9000</value>
  </property>
  ```
  ## 3. hdfs-site.xml
  Insert your username at line 7 & 11
  ```
  <property>
  <name>dfs.replication</name>
  <value>1</value>
  </property>
  <property>
  <name>dfs.namenode.name.dir</name>
  <value>/home/<your_username>/Ecosystem/hadoop-3.3.0/data/namenode</value>
  </property>
  <property>
  <name>dfs.datanode.data.dir</name>
  <value>/home/<your_username>/Ecosystem/hadoop-3.3.0/data/datanode</value>
  </property>
  ```

  

  
  
