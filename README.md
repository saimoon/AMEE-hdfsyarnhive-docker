*** INSTALLATION ***

== CLEAN ALL DOCKER CONTAINERS/IMAGES/VOLUMES ==

# Massive Remove all containers
sudo docker rm -f $(sudo docker ps -a -q)

# Massive Remove all images
sudo docker rmi -f $(sudo docker images -a -q)

# Remove images filtered using regex
sudo docker rmi -f $(sudo docker images | grep -v -E "phusion|bde2020|shawnzhu|^postgres|IMAGE" | awk '{print $3}')

# Remove all stopped containers
sudo docker container prune
# Remove all unused local volumes
sudo docker volume prune

# Remove old volumes directories
sudo rm -rf ./data/namenode ./data/historyserver ./data/datanode1 ./data/datanode2 ./data/datanode3


== PREREQUISITES ==

# Create volumes directories
mkdir -p ./data/namenode ./data/historyserver ./data/datanode1 ./data/datanoe2 ./data/datanode3

# Build Hadoop base image
sudo docker build -t amee/hadoop-base:latest --no-cache --rm hadoop-base/


== DOCKER COMPOSE ==

# Build and Run all containers
sudo docker-compose -f docker-compose-local.yml up --build -d



*** DEVELOPING ***

== HADOOP ==

# Build Hadoop base image
sudo docker build -t amee/hadoop-base:latest --no-cache --rm hadoop-base/

# Build Hadoop datanode image
sudo docker build -t amee/hadoop-datanode:latest --no-cache --rm hadoop-datanode/
# Run Hadoop datanote for test/dev
sudo docker run --name hadoop-datanode -d --rm hadoop-datanode

# Build Hadoop namenode image
sudo docker build -t amee/hadoop-namenode:latest --no-cache --rm hadoop-namenode/
# Run Hadoop namenote for test/dev
sudo docker run --name hadoop-namenode -d --rm hadoop-namenode

# Build Hadoop historyserver image
sudo docker build -t amee/hadoop-historyserver:latest --no-cache --rm hadoop-historyserver/
# Run Hadoop historyserver for test/dev
sudo docker run --name hadoop-historyserver -d --rm hadoop-historyserver

# Build Hadoop nodemanager image
sudo docker build -t amee/hadoop-nodemanager:latest --no-cache --rm hadoop-nodemanager/
# Run Hadoop nodemanager for test/dev
sudo docker run --name hadoop-nodemanager -d --rm hadoop-nodemanager

# Build Hadoop resourcemanager image
sudo docker build -t amee/hadoop-resourcemanager:latest --no-cache --rm hadoop-resourcemanager/
# Run Hadoop resourcemanager for test/dev
sudo docker run --name hadoop-resourcemanager -d --rm hadoop-resourcemanager


== HIVE ==

# Build Hive image
sudo docker build -t amee/hive:latest --no-cache --rm hive/
# Run Hive for test/dev
sudo docker run --name hive -d --rm hive

# Build Hive PostgreSQL image
sudo docker build -t amee/hive-postgresql:latest --no-cache --rm hive-postgresql/
# Run Hive PostgreSQL for test/dev
sudo docker run --name hive-postgresql -d --rm hive-postgresql


