
# Deploy
```
export NAMESPACE=spark
kubectl apply -f spark-cluster.yml --namespace=$NAMESPACE
```
Note: The deployment is optimized for an AWS deployment. An initcontainer add an iptables dropping the AWS metadataservice

# Dockerhub
```
alag/spark-master
alag/spark-worker
```
