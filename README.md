# DemoApp to figure out CNI.

## Commands

```bash
k3d cluster create demo --port "30443:30443@server:0"
kubectl get nodes -o wide
kubectl create secret tls nginx-tls-secret --cert=certs/nginx.crt --key=certs/nginx.key
kubectl apply -f nginx-deployment.yaml
kubectl apply -f nginx-service.yaml
kubectl apply -f nginx-config.yaml
kubectl get svc
kubectl get pods
curl http://localhost:30443
lsof -i | grep 30443
kubectl rollout restart deployment nginx-deployment
```
