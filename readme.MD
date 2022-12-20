To validate services ar connectd to right port.



mahnoor@mahnoor-Latitude-E5470:~/Documents/k8_demo$ kubectl get pod -o wide
NAME                                 READY   STATUS    RESTARTS   AGE     IP           NODE       NOMINATED NODE   READINESS GATES
mongo-deployment-6558588985-v7dx9    1/1     Running   0          2m42s   172.17.0.5   minikube   <none>           <none>
webapp-deployment-7687c99849-xddnv   1/1     Running   0          2m34s   172.17.0.6   minikube   <none>           <none>




mahnoor@mahnoor-Latitude-E5470:~/Documents/k8_demo$ kubectl describe service mongo-service 
Endpoints:         172.17.0.5:27017
 As we can see from above 2 commands mongo-deployment pod has ip of 172.17.0.5 same as mongo-service. Means mongo-service is connected to mongo-deployment pod.

 lets verify webapp-deployment is connected to webapp service.
 mahnoor@mahnoor-Latitude-E5470:~/Documents/k8_demo$ kubectl describe service webapp-service 
 Endpoints:                172.17.0.6:3000


mahnoor@mahnoor-Latitude-E5470:~/Documents/k8_demo$ kubectl get service
NAME             TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)          AGE
kubernetes       ClusterIP   10.96.0.1       <none>        443/TCP          9m33s
mongo-service    ClusterIP   10.105.120.90   <none>        27017/TCP        39s
webapp-service   NodePort    10.110.26.76    <none>        3000:30200/TCP   31s

we want to access webapp from external browser , so in its service we specify type as Nodeport.
now assign this service external ip.

in minikube we can do it using :
$minikube service webapp-service
it will automatically open up browser with service.