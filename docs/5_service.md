### Service
- service > pod
- label selector
```yaml
# kubia-svc.yaml

apiVersion: v1
kind: Service
metadata:
  name: kubia
spec:
  ports:
  - port: 80
  - targetPort: 8080
  selector:
    app: kubia
```

```shell
kubectl get svc
```
```
kubectl get svc
NAME         TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)   AGE
kubernetes   ClusterIP   10.96.0.1       <none>        443/TCP   139d
kubia        ClusterIP   10.98.173.144   <none>        80/TCP    14s
```

```shell
kubectl create -f ../kubernetes/yaml/kubia-svc.yaml
```

```shell
k exec kubia-8645997497-jbr8k -- curl -s http://10.97.100.129
```

### sessionAffinity: ClientIP
- same client -> same redirect
```
spec:
  sessionAffinity: ClientIP
``` 

### multiple port
```
spec:
  ports:
  - name: http
    port: 80
    targetPort: 8080
  - name: https
    port: 443
    targetPort: 8443
```

### multiple port
```
spec:
  ports:
  - name: http
    port: 80
    targetPort: 8080
  - name: https
    port: 443
    targetPort: 8443
```

### naming port (pod)
```
kind: Pod
spec:
  containers:
  - name: kubia
    ports:
    - name: http
      containerPort: 8080
    - name: https
      containerPort: 8443
```
```
kind: Pod
spec:
  containers:
  - name: kubia
    ports:
    - name: http
      containerPort: 8080
    - name: https
      containerPort: 8443
```
```
apiVersion: v1
kind: Service
spec:
  ports:
  - name: http
    port: 80
    targetPort: http
  - name: https
    port: 443
    targetPort: https
```

### FQDN
- https://onlywis.tistory.com/14
- HOST + DOMAIN
- www.naver.com
  - www: HOST
  - naver.com: DOMAIN
- `backend-database.default.svc.cluster.local`

```shell
k exec -it kubia-8645997497-jbr8k bash
```
```
curl http://kubia.default.svc.cluster.local
curl http://kubia.default
curl http://kubia
```
```
cat /etc/resolv.conf

nameserver 10.96.0.10
search default.svc.cluster.local svc.cluster.local cluster.local
options ndots:5
```

### link external
```shell
k describe svc kubia
```
```
Name:              kubia
Namespace:         default
Labels:            <none>
Annotations:       <none>
Selector:          app=kubia
Type:              ClusterIP
IP Family Policy:  SingleStack
IP Families:       IPv4
IP:                10.97.100.129
IPs:               10.97.100.129
Port:              http  80/TCP
TargetPort:        8080/TCP
Endpoints:         172.17.0.12:8080,172.17.0.13:8080,172.17.0.4:8080 + 2 more...
Port:              https  443/TCP
TargetPort:        8443/TCP
Endpoints:         172.17.0.12:8443,172.17.0.13:8443,172.17.0.4:8443 + 2 more...
Session Affinity:  ClientIP
Events:            <none>
```

```shell
k get endpoints kubia
```
```
NAME    ENDPOINTS                                                       AGE
kubia   172.17.0.12:8443,172.17.0.13:8443,172.17.0.4:8443 + 7 more...   131m
```

```shell
cd ../kubernetes/yaml

k create -f external-service.yaml
k create -f external-service-endpoints.yaml
k create -f external-service-externalname.yaml
```