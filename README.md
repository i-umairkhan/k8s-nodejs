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

To test NodePort service:
```
curl $(minikube service k8s-nodejs --url)
```

Now delete NodePort service in order to create LoadBalancer service.
```
kubectl delete service k8s-nodejs
```

Creating LoadBalancer Service
```
kubectl expose deployment k8s-nodejs --type LoadBalancer --port 3000
```
To test LoadBalancer service:
```
curl $(minikube service k8s-nodejs --url)
```

After changing application code to version 2 rebuit docker images and push version 2 to docker hub.
```
sudo docker build -t iumairkhan/k8s-nodejs:2.0.0 .
sudo docker push iumairkhan/k8s-nodejs:2.0.0
```

Now  update deployment image.
```
kubectl set image deployment k8s-nodejs k8s-nodejs=iumairkhan/k8s-nodejs:2.0.0
```

To check status of new deploymenmt:
```
kubectl rollout status deployment k8s-nodejs
```

Now to rollback to old deploymeny.
```
kubectl set image deployment k8s-nodejs k8s-nodejs=iumairkhan/k8s-nodejs
kubectl rollout status deployment k8s-nodejs
```
To get k8s dashboard on minikube node.
```
minikube dashboard
```
Now delete all services in default namespace to use declarative YAML configuration approch.
```
kubectl delete all --all
```
Now creating deployment.yaml to spacify deployment configuration and apply that.
```
kubectl apply -f deploymenmt.yaml
```
Now creating service.yaml to spacify service configuration and apply that.
```
kubectl apply -f service.yaml
```
Now nginx service code is added to create a second deployment.
Building and pushing nginx image to docker hub.
```
sudo docker build -t iumairkhan/k8s-nginx .
sudo docker push iumairkhan/k8s-nginx
```