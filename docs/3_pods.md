### yaml
```
k create -f kubia-manual.yaml #file

k get po kubia-manual -o yaml #out
k get po kubia-manual -o json

k get po

k logs kubia-manual # pod
k logs kubia-manual -c kubia # container

k port-forward kubia-manual 8888:8080
curl localhost:8888
```

### labels
```
k create -f kubia-manual-with-labels.yaml 
k get po --show-labels

k get po --show-labels -L creation_method,env

k label po kubia-manual creation_method=manual
k get po --show-labels -L creation_method,env

k get po --show-labels -l creation
_method=manual

k get po -l env
k get po -l '!env'
```

### namespace(ns)
```
k get ns
k get po -namespace kube-system
k get po -n kube-system

k create -f custom-namespace.yaml
k create ns custom-namespace2

k create -f kubia-manual.yaml -n custom-namespace

alias kcd='k config set-context $(k config current-context) --namespace '
```

### delete
```
k delete po kubia-gpu
k delete po -l creation_method=manual
k delete po -l rel=canary

k delete ns custom-namespace
k delete po --all # don't delete ReplicationController
k delete all --all
```