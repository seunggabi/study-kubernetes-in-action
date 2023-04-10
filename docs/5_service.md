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
