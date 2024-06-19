## Ubuntu Minikube install
```
$ curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
$ sudo install minikube-linux-amd64 /usr/local/bin/minikube

```


```
minikube kubectl -- get po -A
```


```
alias kubectl="minikube kubectl --"
```

```
minikube start
```


```
minikube dashboard
```


#### docker image for minikube

    eval $(minikube docker-env)