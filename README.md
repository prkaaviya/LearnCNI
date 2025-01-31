# DemoApp to figure out CNI

## Commands

```bash
echo "127.0.0.1 demoapp.nginx" | sudo tee -a /etc/hosts
k3d cluster create demo --port "30443:30443@server:0"
kubectl get nodes -o wide
kubectl create secret tls nginx-tls-secret --cert=certs/nginx.crt --key=certs/nginx.key
kubectl apply -f nginx-deployment.yaml
kubectl apply -f nginx-service.yaml
kubectl apply -f nginx-config.yaml
kubectl apply -f nginx-ingressroute.yaml
kubectl get svc
kubectl get pods
curl http://localhost:30443
kubectl rollout restart deployment nginx-deployment
kubectl run debug --rm -it --image=busybox --restart=Never -- nslookup nginx-service.default.svc.cluster.local
```

```bash
$ curl -k https://demoapp.nginx                                  
<!DOCTYPE html>
<html>
<head>
<title>Welcome to nginx!</title>
<style>
html { color-scheme: light dark; }
body { width: 35em; margin: 0 auto;
font-family: Tahoma, Verdana, Arial, sans-serif; }
</style>
</head>
<body>
<h1>Welcome to nginx!</h1>
<p>If you see this page, the nginx web server is successfully installed and
working. Further configuration is required.</p>

<p>For online documentation and support please refer to
<a href="http://nginx.org/">nginx.org</a>.<br/>
Commercial support is available at
<a href="http://nginx.com/">nginx.com</a>.</p>

<p><em>Thank you for using nginx.</em></p>
</body>
</html>
```
