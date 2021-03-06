lesson 1.3.2-run-nginx-with-k8s

1. Run command to enter lesson
$ cd chapter01-basic-knowledges/1.3-basic-kubernetes/02-run-nginx-with-k8s

2. Run command to create namespace
$ kubectl apply -f 00-namespace.yml
namespace/basic-k8s created

3. Check for namespace (basic-k8s)
$ kubectl get ns
NAME              STATUS   AGE
basic-k8s         Active   19s
default           Active   6h40m
kube-node-lease   Active   6h40m
kube-public       Active   6h40m
kube-system       Active   6h40m

4. Create deployment for nginx
$ kubectl apply -f 01-deployment.yml
deployment.apps/nginx created

5. Check for nginx deployment
$ kubectl get pod -n basic-k8s
NAME                     READY   STATUS    RESTARTS   AGE
nginx-86469cbbfd-89cd6   1/1     Running   0          46s

6. Create service for nginx
$ kubectl apply -f 02-service.yml
service/nginx created

7. Check for service nginx
$ kubectl get svc -n basic-k8s
NAME    TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)             AGE
nginx   ClusterIP   10.98.127.130   <none>        8080/TCP,8443/TCP   8s

8. Create ingress rule to nginx service
$ kubectl apply -f 03-ingress.yml
ingress.extensions/ingress created

9. Check for ingress rule (ing = ingress)
$ kubectl get ing -n basic-k8s
NAME      CLASS    HOSTS                        ADDRESS     PORTS   AGE
ingress   <none>   kubernetes.docker.internal   localhost   80      36s

10. Test access service via ingress
$ curl -X GET "http://kubernetes.docker.internal"
<!DOCTYPE html>
<html>
<head>
<title>Welcome to nginx!</title>
<style>
    body {
        width: 35em;
        margin: 0 auto;
        font-family: Tahoma, Verdana, Arial, sans-serif;
    }
</style>
</head>
<body>
<h1>Welcome to nginx!</h1>
<p>If you see this page, the nginx web server is successfully installed and
working. Further configuration is required.</p>

<p>For online documentation and support please refer to
<a href="http://nginx.org/">nginx.org</a>.<br/>
Commercial support is available at
<a href="http://nginx.com/">nginx.com</a>.</p>

<p><em>Thank you for using nginx.</em></p>
</body>
</html>

11. Run command to cleanup
$ kubectl delete ns basic-k8s

12. Run command to exit directory
$ cd ../../../

note
????????? ```curl -X GET "http://kubernetes.docker.internal"``` ????????????????????????????????????????????????????????????????????? host file 
```bash
$ code /private/etc/hosts 
```

```
##
# Host Database
#
# localhost is used to configure the loopback interface
# when the system is booting.  Do not change this entry.
##
127.0.0.1	localhost
255.255.255.255	broadcasthost
::1             localhost
# Added by Docker Desktop
# To allow the same kube context to work on the host and the container:
127.0.0.1 kubernetes.docker.internal
# End of section
```