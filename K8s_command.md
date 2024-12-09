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

**Check the version of specific software in pod**
```
/bin/bash /tmp/k8s_enum_apache_pod.sh
```
```
#!/bin/bash

# Get all pods in the current namespace
pods=$(kubectl get pods -o jsonpath='{.items[*].metadata.name}')

# Header for the output
echo -e "Pod Name\t| Apache Version\t| OpenSSL Version\t| mod_auth_gssapi Version\t| mod_wsgi Version\t| Python Version"

# Iterate through each pod
for pod in $pods; do
  # Check Apache version
  apache_version=$(kubectl exec -it $pod -- sh -c "apache2 -v 2>/dev/null || httpd -v 2>/dev/null" | grep -oP 'Apache/\d+\.\d+\.\d+' || echo "Not installed")

  # Check OpenSSL version
  openssl_version=$(kubectl exec -it $pod -- sh -c "openssl version 2>/dev/null" || echo "Not installed")

  # Check mod_auth_gssapi version
  mod_auth_gssapi_version=$(kubectl exec -it $pod -- sh -c "apache2ctl -M 2>/dev/null || httpd -M 2>/dev/null" | grep -oP 'mod_auth_gssapi/\d+\.\d+\.\d+' || echo "Not detected")

  # Check mod_wsgi version
  mod_wsgi_version=$(kubectl exec -it $pod -- sh -c "apache2ctl -M 2>/dev/null || httpd -M 2>/dev/null" | grep -oP 'mod_wsgi/\d+\.\d+\.\d+' || echo "Not detected")

  # Check Python version
  python_version=$(kubectl exec -it $pod -- sh -c "python3 --version 2>/dev/null || python --version 2>/dev/null" | grep -oP 'Python \d+\.\d+\.\d+' || echo "Not installed")

  # Output the versions
  echo -e "$pod\t| $apache_version\t| $openssl_version\t| $mod_auth_gssapi_version\t| $mod_wsgi_version\t| $python_version"
done

```
