### docs
- https://github.com/kubernetes/minikube
    - https://minikube.sigs.k8s.io/docs/start/
- https://kubernetes.io/ko/docs/tasks/tools/included/optional-kubectl-configs-zsh/
- https://stackoverflow.com/questions/64306744/error-when-trying-to-expose-a-docker-container-in-minikube

### depth
```
cluster > node > worker > pod > container
```

### alias
- https://kubernetes.io/ko/docs/tasks/tools/included/optional-kubectl-configs-zsh/
```shell
source <(kubectl completion zsh)

echo 'alias k=kubectl' >>~/.zshrc
echo "alias kgp='k get pods -o wide'" >>~/.zshrc
echo "alias kgs='k get svc'" >>~/.zshrc
echo "alias kgr='k get rs'" >>~/.zshrc
echo "alias kdp='k describe pod'" >>~/.zshrc
echo 'compdef __start_kubectl k' >>~/.zshrc
```

### start
```shell
brew install minikube
minikube start
kubectl cluster-info

➜  nodejs git:(main) ✗ kubectl cluster-info
Kubernetes control plane is running at https://127.0.0.1:59122
CoreDNS is running at https://127.0.0.1:59122/api/v1/namespaces/kube-system/services/kube-dns:dns/proxy
```
```shell
➜  nodejs git:(main) ✗ kubectl get nodes
NAME       STATUS   ROLES                  AGE     VERSION
minikube   Ready    control-plane,master   2m13s   v1.23.3
```
```shell
kubectl describe node minikube
Name:               minikube
Roles:              control-plane,master
Labels:             beta.kubernetes.io/arch=arm64
                    beta.kubernetes.io/os=linux
                    kubernetes.io/arch=arm64
                    kubernetes.io/hostname=minikube
                    kubernetes.io/os=linux
                    minikube.k8s.io/commit=362d5fdc0a3dbee389b3d3f1034e8023e72bd3a7
                    minikube.k8s.io/name=minikube
                    minikube.k8s.io/primary=true
                    minikube.k8s.io/updated_at=2022_04_25T15_09_15_0700
                    minikube.k8s.io/version=v1.25.2
                    node-role.kubernetes.io/control-plane=
                    node-role.kubernetes.io/master=
                    node.kubernetes.io/exclude-from-external-load-balancers=
Annotations:        kubeadm.alpha.kubernetes.io/cri-socket: /var/run/dockershim.sock
                    node.alpha.kubernetes.io/ttl: 0
                    volumes.kubernetes.io/controller-managed-attach-detach: true
CreationTimestamp:  Mon, 25 Apr 2022 15:09:13 +0900
Taints:             <none>
Unschedulable:      false
Lease:
  HolderIdentity:  minikube
  AcquireTime:     <unset>
  RenewTime:       Mon, 25 Apr 2022 15:12:20 +0900
Conditions:
  Type             Status  LastHeartbeatTime                 LastTransitionTime                Reason                       Message
  ----             ------  -----------------                 ------------------                ------                       -------
  MemoryPressure   False   Mon, 25 Apr 2022 15:09:16 +0900   Mon, 25 Apr 2022 15:09:11 +0900   KubeletHasSufficientMemory   kubelet has sufficient memory available
  DiskPressure     False   Mon, 25 Apr 2022 15:09:16 +0900   Mon, 25 Apr 2022 15:09:11 +0900   KubeletHasNoDiskPressure     kubelet has no disk pressure
  PIDPressure      False   Mon, 25 Apr 2022 15:09:16 +0900   Mon, 25 Apr 2022 15:09:11 +0900   KubeletHasSufficientPID      kubelet has sufficient PID available
  Ready            True    Mon, 25 Apr 2022 15:09:16 +0900   Mon, 25 Apr 2022 15:09:16 +0900   KubeletReady                 kubelet is posting ready status
Addresses:
  InternalIP:  192.168.49.2
  Hostname:    minikube
Capacity:
  cpu:                5
  ephemeral-storage:  61255492Ki
  hugepages-1Gi:      0
  hugepages-2Mi:      0
  hugepages-32Mi:     0
  hugepages-64Ki:     0
  memory:             8039792Ki
  pods:               110
Allocatable:
  cpu:                5
  ephemeral-storage:  61255492Ki
  hugepages-1Gi:      0
  hugepages-2Mi:      0
  hugepages-32Mi:     0
  hugepages-64Ki:     0
  memory:             8039792Ki
  pods:               110
System Info:
  Machine ID:                 7f42765e713c4b909dde4d5f15b8d18f
  System UUID:                7f42765e713c4b909dde4d5f15b8d18f
  Boot ID:                    259eb30d-0111-4863-96ff-ea939174841c
  Kernel Version:             5.10.104-linuxkit
  OS Image:                   Ubuntu 20.04.2 LTS
  Operating System:           linux
  Architecture:               arm64
  Container Runtime Version:  docker://20.10.12
  Kubelet Version:            v1.23.3
  Kube-Proxy Version:         v1.23.3
PodCIDR:                      10.244.0.0/24
PodCIDRs:                     10.244.0.0/24
Non-terminated Pods:          (7 in total)
  Namespace                   Name                                CPU Requests  CPU Limits  Memory Requests  Memory Limits  Age
  ---------                   ----                                ------------  ----------  ---------------  -------------  ---
  kube-system                 coredns-64897985d-72bfs             100m (2%)     0 (0%)      70Mi (0%)        170Mi (2%)     2m59s
  kube-system                 etcd-minikube                       100m (2%)     0 (0%)      100Mi (1%)       0 (0%)         3m13s
  kube-system                 kube-apiserver-minikube             250m (5%)     0 (0%)      0 (0%)           0 (0%)         3m13s
  kube-system                 kube-controller-manager-minikube    200m (4%)     0 (0%)      0 (0%)           0 (0%)         3m14s
  kube-system                 kube-proxy-tbszk                    0 (0%)        0 (0%)      0 (0%)           0 (0%)         2m59s
  kube-system                 kube-scheduler-minikube             100m (2%)     0 (0%)      0 (0%)           0 (0%)         3m13s
  kube-system                 storage-provisioner                 0 (0%)        0 (0%)      0 (0%)           0 (0%)         3m10s
Allocated resources:
  (Total limits may be over 100 percent, i.e., overcommitted.)
  Resource           Requests    Limits
  --------           --------    ------
  cpu                750m (15%)  0 (0%)
  memory             170Mi (2%)  170Mi (2%)
  ephemeral-storage  0 (0%)      0 (0%)
  hugepages-1Gi      0 (0%)      0 (0%)
  hugepages-2Mi      0 (0%)      0 (0%)
  hugepages-32Mi     0 (0%)      0 (0%)
  hugepages-64Ki     0 (0%)      0 (0%)
Events:
  Type    Reason                   Age    From        Message
  ----    ------                   ----   ----        -------
  Normal  Starting                 2m57s  kube-proxy
  Normal  Starting                 3m12s  kubelet     Starting kubelet.
  Normal  NodeHasSufficientMemory  3m11s  kubelet     Node minikube status is now: NodeHasSufficientMemory
  Normal  NodeHasNoDiskPressure    3m11s  kubelet     Node minikube status is now: NodeHasNoDiskPressure
  Normal  NodeHasSufficientPID     3m11s  kubelet     Node minikube status is now: NodeHasSufficientPID
  Normal  NodeAllocatableEnforced  3m11s  kubelet     Updated Node Allocatable limit across pods
  Normal  NodeReady                3m11s  kubelet     Node minikube status is now: NodeReady
```

#### kubia.yaml
- https://kubernetes.io/ko/docs/concepts/workloads/controllers/deployment/
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: kubia
spec:
  replicas: 3
  selector:
    matchLabels:
      app: kubia
  template:
    metadata:
      labels:
        app: kubia
    spec:
      containers:
        - name: kubia
          image: seunggab/kubia:latest
          ports:
          - containerPort: 8080
```

### shell
- https://minikube.sigs.k8s.io/docs/handbook/accessing/#using-minikube-tunnel
```shell
kubectl apply -f ../k8s/kubia.yaml
kubectl expose deployment kubia --type=LoadBalancer --port 8080 --name kubia-http

minikube tunnel &

curl 127.0.0.1:8080
```

---

### if you change `replicas`
1. change `kubia.yaml` (3 -> 5)
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: kubia
spec:
  replicas: 5
  selector:
    matchLabels:
      app: kubia
  template:
    metadata:
      labels:
        app: kubia
    spec:
      containers:
        - name: kubia
          image: seunggab/kubia:latest
          ports:
          - containerPort: 8080
```
2. re-apply
```shell
kubectl apply -f kubia.yaml

# as-is
NAME                     READY   STATUS    RESTARTS   AGE
kubia-5f896dc5d5-qp7wl   1/1     Running   0          20s
kubia-5f896dc5d5-rqqm5   1/1     Running   0          20s
kubia-5f896dc5d5-vqgj9   1/1     Running   0          20s

# to-be
NAME                     READY   STATUS              RESTARTS   AGE
kubia-5f896dc5d5-fsd49   0/1     ContainerCreating   0          6s
kubia-5f896dc5d5-qp7wl   1/1     Running             0          3m35s
kubia-5f896dc5d5-rqqm5   1/1     Running             0          3m35s
kubia-5f896dc5d5-vqgj9   1/1     Running             0          3m35s
kubia-5f896dc5d5-x84fr   1/1     Running             0          6s
```

### dashboard
- http://127.0.0.1:52445/api/v1/namespaces/kubernetes-dashboard/services/http:kubernetes-dashboard:/proxy/#/workloads?namespace=default
```
minikube dashboard
```

### ref
- https://stackoverflow.com/questions/64306744/error-when-trying-to-expose-a-docker-container-in-minikube/71996168#71996168