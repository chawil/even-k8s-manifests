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

# if using a remote kubernetes
k3d kubeconfig get test
# this remote config to save in a local file
KUBECONFIG=~/.kube/config:/c/temp/oo-k3d kubectl config view --flatten > ~/.kube/new_config
# check file
mv ~/.kube/new_config ~/.kube/config
# be sure the server is reachable from local

# you can list the contexts
kubectl config get-contexts
# and select one
kubectl config set-context k3d-test

# get the logs from all replicas
kubectl logs -n even -l app=api-even -f
```

## other knowledge

- k3d uses docker, if your docker/host already use port 80, a LoadBalancer with port 80 will stay in pending mode
- from https://kubernetes.io/docs/concepts/workloads/pods/pod-lifecycle/
  - livenessProbe: Indicates whether the container is running.
  - readinessProbe: Indicates whether the container is ready to respond to requests.
  - startupProbe: Indicates whether the application within the container is started.
