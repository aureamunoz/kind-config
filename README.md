# Kubernetes kind configuration 

This project explains and contains instructions to set up a K8s cluster using `kind` 
and next to provision it with a docker registry, dashboard, ingress controller, ...

### Prerequisites

- [Docker client](https://docs.docker.com/desktop/)
- [Kind](https://kind.sigs.k8s.io/docs/user/quick-start/)
- [Kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/)

### Create the Kind cluster

Execute the following bash script to create a Kind cluster having a docker registry and ingress controller
```bash
./kind-reg-ingress.sh devcluster
```

### Deploy the OKD console

Create the `dashboard` namespace
```bash
kubectl create ns dashboard
```
Next deploy the K8s resources
```bash
kubectl apply -f okd-console/
```
Wait a few moments and next open the console within your browser `http://console.127.0.0.1.nip.io/` 

### Install OLM

Execute the following command to deploy the Operators Lifecycle Managers
```bash
kubectl create -f https://raw.githubusercontent.com/operator-framework/operator-lifecycle-manager/master/deploy/upstream/quickstart/crds.yaml
kubectl create -f https://raw.githubusercontent.com/operator-framework/operator-lifecycle-manager/master/deploy/upstream/quickstart/olm.yaml
```


