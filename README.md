# Streaming Visualization Demo

## 0. Prerequisites
- Node: >= 11.11.0
- NPM: >= 6.7.0
- Docker

## 1. Initial Setup

### Setup Kafka with topic
```bash
docker run --name kafka_vis -d -p 2181:2181 -p 9092:9092 --env ADVERTISED_HOST=0.0.0.0 --env ADVERTISED_PORT=9092 spotify/kafka
docker ps -a
# create new topic
docker exec -i -t kafka_vis /opt/kafka_2.11-0.10.1.0/bin/kafka-topics.sh --create --zookeeper localhost:2181 --replication-factor 1 --partitions 1 --topic test3
```

### Setup Redis
```bash
docker run -d -p 6379:6379 redis
```

### Get libraries
```bash
npm install
```


## 2. Running this web app (from root project directory)
```bash
node server.js
```

## 3. Generate data
Run Spark Streaming Datagenerator and Spark Streaming Processor jobs to generate data with classifications
These are separate projects

Alternatively, just run the included script to simulate this process:

3a. Install redis-cli

Mac (via brew):
```bash
brew install redis
```
Windows:
https://github.com/rgl/redis/downloads

Unix:
```
wget http://download.redis.io/redis-stable.tar.gz
tar xvzf redis-stable.tar.gz
cd redis-stable
make
   ```

3b. Run data generation script (from root of project)
```bash
redis-cli < scripts/coords.txt

```

