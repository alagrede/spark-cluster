#Build
docker build -t alag/spark-worker:2.3.1-hadoop2.7 .

#Deploy
docker login (register on: https://hub.docker.com)
docker push alag/spark-worker