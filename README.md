# Requested topics 

<img src="topic.png">

## Controllers in k8s 

<img src="cloudcont.png">

## Replication controller in k8s 

### Deployment using 
<img src="dep.png">

### cleaning namespaces ---

```

 fire@ashutoshhs-MacBook-Air  ~/Desktop/k8sapps  kubectl  config get-contexts 
CURRENT   NAME                          CLUSTER      AUTHINFO           NAMESPACE
*         kubernetes-admin@kubernetes   kubernetes   kubernetes-admin   ashu-project
 fire@ashutoshhs-MacBook-Air  ~/Desktop/k8sapps  kubectl get  all
No resources found in ashu-project namespace.
 fire@ashutoshhs-MacBook-Air  ~/Desktop/k8sapps  kubectl  delete all --all
No resources found
 fire@ashutoshhs-MacBook-Air  ~/Desktop/k8sapps  

```
### Deployment creationg 

### Templates in deploy 

<img src="temp.png">

### Deployment creation --

```
kubectl  apply -f  nodedeploy.yaml
deployment.apps/ashuapp created
 fire@ashutoshhs-MacBook-Air  ~/Desktop/k8sapps  kubectl  get deployment
NAME      READY   UP-TO-DATE   AVAILABLE   AGE
ashuapp   1/1     1            1           38s
 fire@ashutoshhs-MacBook-Air  ~/Desktop/k8sapps  kubectl  get deploy    
NAME      READY   UP-TO-DATE   AVAILABLE   AGE
ashuapp   1/1     1            1           49s
 fire@ashutoshhs-MacBook-Air  ~/Desktop/k8sapps  kubectl  get  po   
NAME                       READY   STATUS    RESTARTS   AGE
ashuapp-85d97994f9-8hggg   1/1     Running   0          60s

```

### Replication controller will maintain copy of pod --

```
kubectl delete pod ashuapp-85d97994f9-8hggg
pod "ashuapp-85d97994f9-8hggg" deleted
 fire@ashutoshhs-MacBook-Air  ~/Desktop/k8sapps  kubectl  get  po -o wide                    
NAME                       READY   STATUS    RESTARTS   AGE   IP               NODE    NOMINATED NODE   READINESS GATES
ashuapp-85d97994f9-vw8kj   1/1     Running   0          25s   192.168.135.20   node3   <none>           <none>

```

### manual scaling --

```
      4m59s
 fire@ashutoshhs-MacBook-Air  ~/Desktop/k8sapps  kubectl  scale  deployment  ashuapp  --replicas=3 
deployment.apps/ashuapp scaled
 fire@ashutoshhs-MacBook-Air  ~/Desktop/k8sapps  kubectl  get po 
NAME                       READY   STATUS    RESTARTS   AGE
ashuapp-85d97994f9-2w5kl   1/1     Running   0          7s
ashuapp-85d97994f9-sphq2   1/1     Running   0          7s
ashuapp-85d97994f9-vw8kj   1/1     Running   0          7m54s
 fire@ashutoshhs-MacBook-Air  ~/Desktop/k8sapps  kubectl  get po -o wide
NAME                       READY   STATUS    RESTARTS   AGE     IP                NODE    NOMINATED NODE   READINESS GATES
ashuapp-85d97994f9-2w5kl   1/1     Running   0          12s     192.168.104.60    node2   <none>           <none>
ashuapp-85d97994f9-sphq2   1/1     Running   0          12s     192.168.166.139   node1   <none>           <none>
ashuapp-85d97994f9-vw8kj   1/1     Running   0          7m59s   192.168.135.20    node3   <none>           <none>

```

### service creation method --

<img src="svc1.png">

```
 
 fire@ashutoshhs-MacBook-Air  ~/Desktop/k8sapps  kubectl  get  deploy 
NAME      READY   UP-TO-DATE   AVAILABLE   AGE
ashuapp   3/3     3            3           16m
 fire@ashutoshhs-MacBook-Air  ~/Desktop/k8sapps  kubectl  get  svc
No resources found in ashu-project namespace.
 fire@ashutoshhs-MacBook-Air  ~/Desktop/k8sapps  kubectl  expose deployment  ashuapp --type NodePort --port 3000 --name  ashusvc1                           
service/ashusvc1 exposed
 fire@ashutoshhs-MacBook-Air  ~/Desktop/k8sapps  kubectl  get  svc 
NAME       TYPE       CLUSTER-IP     EXTERNAL-IP   PORT(S)          AGE
ashusvc1   NodePort   10.111.33.32   <none>        3000:31148/TCP   5s

```

### Deploy custom yaml -- 

```
kubectl apply -f nodedeploy.yaml   
namespace/x1 configured
deployment.apps/ashuapp configured
service/s1 configured
 fire@ashutoshhs-MacBook-Air  ~/Desktop/k8sapps  kubectl  get  deploy,pod,svc -n x1 
NAME                      READY   UP-TO-DATE   AVAILABLE   AGE
deployment.apps/ashuapp   1/1     1            1           58s

NAME                           READY   STATUS    RESTARTS   AGE
pod/ashuapp-85d97994f9-l58k9   1/1     Running   0          59s

NAME         TYPE       CLUSTER-IP     EXTERNAL-IP   PORT(S)          AGE
service/s1   NodePort   10.96.80.203   <none>        1234:31277/TCP   58s
 fire@ashutoshhs-MacBook-Air  ~/Desktop/k8sapps  kubectl delete  -f nodedeploy.yaml
namespace "x1" deleted
deployment.apps "ashuapp" deleted
service "s1" deleted

```




