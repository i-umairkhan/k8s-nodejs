Build and push image to dockerhub.
```
sudo docker build -t iumairkhan/k8s-nodejs .
sudo docker push iumairkhan/k8s-nodejs
```
Create Deployment in minikube node.
```
kubectl create deployment k8s-nodejs --image iumairkhan/k8s-nodejs
```
Create ClusterIP service for deployment
```
kubectl expose deployment k8s-nodejs --port 3000
```