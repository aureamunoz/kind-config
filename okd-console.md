# Steps to follow to install on kind the okd console

- Create a serviceaccount for the console
  ```bash
  kubectl apply -f console/01-serviceaccount.yml
  ```
- Before to install the console, it is first needed to get from the k8s cluster the secretname of the default user needed to let the UI to access
  the API and next to specify it within the deployment yaml resource
  ```bash
  SECRET_NAME=$(kubectl get serviceaccount console --namespace=kube-system -o jsonpath='{.secrets[0].name}')
  file_contents=$(<deployment.yml.tmpl)
  echo "${file_contents//SECRETNAME/$SECRET_NAME}" > console/01-deployment.yml
  ```
- To deploy the okd console, service and ingress route
  ```bash
  kubectl apply -f console/
  ```
- To delete the okd console, service, ...
  ```bash
  kubectl delete -f console/
  ```
