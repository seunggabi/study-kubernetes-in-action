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

