Build and push image to dockerhub.
```
sudo docker build -t iumairkhan/k8s-nodejs .
sudo docker push iumairkhan/k8s-nodejs
```
Create Deployment in minikube node.
```
kubectl create deployment k8s-nodejs --image iumairkhan/k8s-nodejs
```
Create ClusterIP service for deployment.
```
kubectl expose deployment k8s-nodejs --port 3000
```

Scale deployment to 4 replicas.

```
kubectl scale deployment k8s-nodejs --replicas 4
```

ClusterIP is used for internel connectivity so delete it.
```
kubectl delete service k8s-nodejs
```

Now create NodePort service for external connectivity.
```
kubectl expose deployment k8s-nodejs --type NodePort --port 3000
```

Now to get external IP url:
```
minikube service k8s-nodejs
```

To test deployment:
```
curl $(minikube service k8s-nodejs --url)
```