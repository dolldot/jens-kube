# jens-kube

## Requirements
- minikube
- helm

## How To Run
1. Installing
```
$ kubectl apply -f setup/jenkins-namespace.yaml
$ kubectl apply -f setup/jenkins-volume.yaml -n jenkins
$ helm install jenkins -f values.yaml stable/jenkins -n jenkins
```
2. Run Jenkins
```
To get password
$ printf $(kubectl get secret --namespace jenkins jenkins -o jsonpath="{.data.jenkins-admin-password}" | base64 --decode);echo

Get pod name
$ export POD_NAME=$(kubectl get pods --namespace jenkins -l "app.kubernetes.io/component=jenkins-master" -l "app.kubernetes.io/instance=jenkins" -o jsonpath="{.items[0].metadata.name}")

Port forwarding to access from local
$ kubectl --namespace jenkins port-forward $POD_NAME 8080:8080
```
