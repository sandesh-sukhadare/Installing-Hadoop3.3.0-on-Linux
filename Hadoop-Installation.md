# Installing Hadoop on Linux (Ubuntu)

### Install OpenJDK
  ```
  sudo apt install openjdk-8-jdk -y
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
