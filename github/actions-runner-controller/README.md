# Actions Runner Controller (ARC)

## Prerequisites

Install [cert-manager](https://github.com/cert-manager/cert-manager).

Kubectl deployment

```
kubectl apply -f https://github.com/cert-manager/cert-manager/releases/download/v1.10.0/cert-manager.yaml
```

Helm deployment

https://cert-manager.io/docs/installation/helm/#installing-with-helm

Before installing the chart, you must first install the cert-manager CustomResourceDefinition resources. This is performed in a separate step to allow you to easily uninstall and reinstall cert-manager without deleting your installed custom resources.

```
kubectl apply -f https://github.com/cert-manager/cert-manager/releases/download/v1.10.0/cert-manager.crds.yaml
```

`cert-manager.yaml` is also placed in this repository.

```
helm repo add jetstack https://charts.jetstack.io
```

```
helm install my-release --namespace cert-manager --version v1.10.0 jetstack/cert-manager
```

Helm add repository for cert-manager.

```
helm repo add actions-runner-controller https://actions-runner-controller.github.io/actions-runner-controller
```

Helm install ARC.

```
helm upgrade --install --namespace actions-runner-system --create-namespace\
  --set=authSecret.create=true\
  --set=authSecret.github_token="REPLACE_YOUR_TOKEN_HERE"\
  --wait actions-runner-controller actions-runner-controller/actions-runner-controller
```