# even-k8s-manifests

Even system manifests

## objectives

- have manifests you can kubectl apply on a fresh k3s instance
- have some helm to set up the useful stuff (certificate issuer, simple router like nginx, and more...)

## links

- https://kubernetes.io/docs/tasks/access-application-cluster/connecting-frontend-backend/
- https://k3d.io/ probably the fastest way to have a running kubernetes cluster up and running (k3s in docker)
- https://wsl.dev/wsl2-k3d-arkade/ some nice things including arkade

## logs

```bash
# not including installation steps
wsl
sudo service docker start
k3d cluster create test
kubectl apply -f example.yml
kubectl port-forward -n even svc/api-even-front 8080:80
# open broswer and test api calls http://localhost:8080/home/

# you can check logs
kubectl logs -n even service/api-even
kubectl logs -n even service/api-even-front
```
