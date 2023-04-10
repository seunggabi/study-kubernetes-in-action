### ReplicationController
```
k create -f kubia-rc.yaml
k delete -f kubia-rc.yaml

k delete pods kubia-r87z4
k get rc

k describe rc kubia
k get node
k get nodes

k label pod kubia-wnpxl type=special
k get po
```
```
k get pods --show-labels
NAME          READY   STATUS    RESTARTS   AGE   LABELS
kubia-kz2j5   1/1     Running   0          17m   app=kubia
kubia-tk4km   1/1     Running   0          17m   app=kubia
kubia-wnpxl   1/1     Running   0          12m   app=kubia,type=special

k label po kubia-wnpxl app=foo --overwrite
NAME          READY   STATUS    RESTARTS   AGE   LABELS
kubia-9z6gn   1/1     Running   0          12s   app=kubia
kubia-kz2j5   1/1     Running   0          19m   app=kubia
kubia-tk4km   1/1     Running   0          19m   app=kubia
kubia-wnpxl   1/1     Running   0          13m   app=foo,type=special
```
```
k get po -L app
NAME          READY   STATUS    RESTARTS   AGE   APP
kubia-9z6gn   1/1     Running   0          46s   kubia
kubia-kz2j5   1/1     Running   0          19m   kubia
kubia-tk4km   1/1     Running   0          19m   kubia
kubia-wnpxl   1/1     Running   0          13m   foo
```
```
k edit rc kubia
k scale rc kubia --replicas=2
k delete po -l app=kubia

kgp # k get po
NAME          READY   STATUS    RESTARTS   AGE     IP            NODE       NOMINATED NODE   READINESS GATES
kubia-m6sp8   1/1     Running   0          3m41s   172.17.0.18   minikube   <none>           <none>
kubia-wnpxl   1/1     Running   0          24m     172.17.0.14   minikube   <none>           <none>
```
```
k delete rc kubia 
k delete rc kubia --cascade=false
```

---

### ReplicaSet
- `apiVersion: apps/v1`
- `env=*`
```
k create -f kubia-rs.yaml
k get rs
k descirbe rs
Name:         kubia
Namespace:    default
Selector:     app=kubia
Labels:       <none>
Annotations:  <none>
Replicas:     3 current / 3 desired
Pods Status:  3 Running / 0 Waiting / 0 Succeeded / 0 Failed
Pod Template:
  Labels:  app=kubia
  Containers:
   kubia:
    Image:        luksa/kubia
    Port:         <none>
    Host Port:    <none>
    Environment:  <none>
    Mounts:       <none>
  Volumes:        <none>
Events:
  Type    Reason            Age   From                   Message
  ----    ------            ----  ----                   -------
  Normal  SuccessfulCreate  64s   replicaset-controller  Created pod: kubia-27fjc
  Normal  SuccessfulCreate  64s   replicaset-controller  Created pod: kubia-dgjll
  Normal  SuccessfulCreate  64s   replicaset-controller  Created pod: kubia-m87jm
```
```
k delete -f kubia-rs.yaml
k delete rs kubia
```

---

### DaemonSet
```
k create -f ssd-monitor-daemonset.yml
k get ds # DaemonSet

k get po
No resources found in default namespace.

k get node
NAME       STATUS   ROLES                  AGE   VERSION
minikube   Ready    control-plane,master   13d   v1.23.3

k label node minikube disk=ssd

k label node minikube disk=hdd --overwrite
```

---

### Job
```
k get jobs
k get po
k logs batch-job-sdjzq

k create -f multi-completion-batch-job.yaml
k create -f multi-completion-parallel-batch-job.yaml
```
```
k scale job multi-completion-batch-job --replicas 3
```