**Get all pods information***
kubectl get pods

**Ensure the pod you want to access is in the Running state:**
```
kubectl get pods -o wide
```
**Access a Pod via Shell**
```
kubectl exec -it <pod-name> -- /bin/bash
kubectl exec -it <pod-name> -- /bin/sh
```

**List Pods Across All Namespaces**
```
kubectl get pods --all-namespaces
```

**List Services in the Namespace:**
```
kubectl get services
kubectl describe service <service-name>
```
**Identify Pods Running Specific Process**
```
kubectl exec -it <pod-name> -- ps aux | grep apache
kubectl exec -it <pod-name> -- ps aux | grep httpd
kubectl get pods -o=jsonpath="{.items[*].spec.containers[*].image}" | grep httpd
kubectl logs <pod-name> | grep Apache


```

**Check Pod Logs: Access the logs of pods that match the service selector to trace the API request.**
```
kubectl logs <pod-name>
kubectl logs <pod-name> -c <container-name>
```

**Search for the File**
```
kubectl exec -it <pod-name> -- find / -name <file-name> 2>/dev/null
kubectl exec -it <pod-name> -- grep -r '<pattern>' /path/to/search 2>/dev/null
kubectl exec -it <pod-name> -- ls -l /path/to/directory 2>/dev/null
kubectl exec -it <pod-name> -- find /etc /var /usr -name <file-name>


```
```
for pod in $(kubectl get pods -o jsonpath='{.items[*].metadata.name}'); do
  echo "Searching in $pod..."
  kubectl exec -it $pod -- find / -name <file-name> 2>/dev/null
done
```
