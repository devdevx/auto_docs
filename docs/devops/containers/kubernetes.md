# Kubernetes

## Links

(Should i use K8s?)[https://thenewstack.io/kubernetes-isnt-always-the-right-choice/]

## Install `kubectl`

### Debian

``` bash
sudo apt-get install gnupg2
sudo apt-get update && sudo apt-get install -y apt-transport-https
curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add -
echo "deb https://apt.kubernetes.io/ kubernetes-xenial main" | sudo tee -a /etc/apt/sources.list.d/kubernetes.list
sudo apt-get update
sudo apt-get install -y kubectl
```

### Ubuntu

```bash
sudo apt-get install kubectl
```

## Commands

List contexts

````
kubectl config get-contexts
````

Switch context

````
kubectl config use-context <CONTEXT_NAME>
````

Rename context

````
kubectl config rename-context <OLD_NAME> <NEW_NAME>
````

Create manifest (Imperative)

````
kubectl create -f manifest.yaml
````

Apply manifest (Declarative)

````
kubectl apply -f manifest.yaml
````

Show resources

````
kubectl get nodes
kubectl get pods
kubectl get rs
kubectl get deployments
kubectl get svc
kubectl get ingress
kubectl get serviceaccount
kubectl get netpol
````

Delete manifest

````
kubectl delete manifes.yaml
````

Show namespaces with labels

````
kubectl get namespaces --show-labels
````

Add lable to namespace

````
 kubectl label namespace default istio-injection=enabled
````

Rolling updates

````
kubectl apply -f file.yaml --record
kubectl rollout history deployment/name
kubectl rollout history deployment/name --revision=1
kubectl rollout undo deployment/name
kubectl rollout undo deployment/name --to-revision=1
````

See logs

```
kubectl logs -f POD_NAME
```

Execute shell

````
kubectl exec -it nginx -- /bin/bash
````

Port forward

```
kubectl port-forward deployments/deployment local_port:image_port
kubectl port-forward pod local_port:image_port
```

Proxy

````
kubectl proxy
http://localhost:8001/api/v1/proxy/namespaces/<NAMESPACE>/services/<SERVICE_NAME>/proxy/
````

## Pods

### Envs from spec

````yaml
apiVersion: v1
kind: Pod
metadata:
  name: dapi-envars-fieldref
spec:
  containers:
    - name: test-container
      image: k8s.gcr.io/busybox
      env:
        - name: MY_POD_NAME
          valueFrom:
            fieldRef:
              fieldPath: metadata.name
````

### Resources

````yaml
apiVersion: v1
kind: Pod
metadata:
  name: my-pod
spec:
  containers:
  - name: my-container
    image: image
    resources:
      requests:
        memory: "64Mi"
        cpu: "250m"
      limits:
        memory: "128Mi"
        cpu: "500m"
````

### Probes

````yaml
apiVersion: v1
kind: Pod
metadata:
  name: goproxy
  labels:
    app: goproxy
spec:
  containers:
  - name: goproxy
    image: k8s.gcr.io/goproxy:0.1
    ports:
    - containerPort: 8080
    readinessProbe:
      tcpSocket:
        port: 8080
      initialDelaySeconds: 5
      periodSeconds: 10
    livenessProbe:
      tcpSocket:
        port: 8080
      initialDelaySeconds: 15
      periodSeconds: 20
````

### Multi container

Only recommended for specific cases. In this example is required to extract the logs from the main container.

````yaml
apiVersion: v1                                 
kind: Pod                                      
metadata:                                      
  name: exim                                   
spec:                                          
  containers:                                  
    - name: exim                               
      image: dodemoorg/exim:1.3                
      env:                                     
        - name: domain                         
          value: example.local                 
        - name: root_alias                     
          value: youraddress@example.local     
        - name: queue_time                     
          value: 1m                            
      volumeMounts:                            
        - mountPath: /var/log/exim4            
          name: logs                           
    - name: filebeats                          
      image: dodemoorg/eximbeats:1.3           
      volumeMounts:                            
        - mountPath: /var/log/exim4            
          name: logs                           
  volumes:                                     
    - name: logs                               
      emptyDir: {}                             
````

### InitContainer

````yaml
apiVersion: v1                                                                                      
kind: Pod                                                                                           
metadata:                                                                                           
  name: octopress                                                                                   
spec:                                                                                               
  initContainers:                                                                                   
    - name: octopress                                                                               
      image: registry.gitlab.com/perlstalker/octopress-deploy                                       
      volumeMounts:                                                                                 
        - mountPath: /public                                                                        
          name: docroot                                                                             
  containers:                                                                                       
    - name: web                                                                                     
      image: nginx:1.13.6                                                                           
      ports:                                                                                        
        - containerPort: 80                                                                         
      volumeMounts:                                                                                 
        - mountPath: /usr/share/nginx/html                                                          
          name: docroot                                                                             
  volumes:                                                                                          
    - name: docroot                                                                                 
      emptyDir: {}                                                                                  
````

## Job

````yaml
apiVersion: batch/v1
kind: Job
metadata:
  name: hello
spec:
  template:
    metadata:
      name: hello
    spec:
      containers:
        - name: hello
          image: debian:9
          command: ["echo", "Hello world!"]
      restartPolicy: OnFailure
````

## CronJob

````yaml
apiVersion: batch/v1beta1                          
kind: CronJob                                      
metadata:                                          
  name: hello                                      
spec:                                              
  schedule: "*/1 * * * *"                          
  jobTemplate:                                     
    metadata:                                      
      name: hello                                  
    spec:                                          
      template:                                    
        spec:                                      
          containers:                              
            - name: hello                          
              image: debian:9                      
              command: ["echo", "Hello world!"]    
          restartPolicy: Never                
````

## Secrets

````yaml
apiVersion: v1
kind: Secret
metadata:
  name: passwords
data:
  dbpass: cGFzc3dvcmQ= #b64
  rootpass: ZGZqbCQ0OTRxbGtsJCUlXl4=
````

Create secret from console:

````
kubectl create secret generic test-secret --from-literal=username='my-app' --from-literal=password='39528$vdg7Jb'
````

Using a value of `Secret` in `env`:

````yaml
apiVersion: v1
kind: Pod
metadata:
  name: secretenv
spec:
  containers:
    - name: busybox
      image: busybox:1.27.2
      env:
        - name: DB_PASSWORD
          valueFrom:
            secretKeyRef:
              name: passwords
              key: dbpass
        - name: ROOT_PASSWORD
          valueFrom:
            secretKeyRef:
              name: passwords
              key: rootpass
````

Using all values of `Secret` in `env`:

````yaml
apiVersion: v1
kind: Pod
metadata:
  name: envfrom-secret
spec:
  containers:
  - name: envars-test-container
    image: nginx
    envFrom:
    - secretRef:
        name: passwords
````

Using a value of `Secret` in `volume`:

````yaml
apiVersion: v1
kind: Pod
metadata:
  name: secretvol
spec:
  volumes:
    - name: password-volume
      secret:
        secretName: passwords
  containers:
    - name: busybox
      image: busybox:1.27.2
      volumeMounts:
        - name: password-volume
          mountPath: /etc/passwords
````

## ConfigMaps

````yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: testconf
  namespace: default
data:
  test: value
````

Using a value of `ConfigMap` in `env`:

````yaml
apiVersion: v1
kind: Pod
metadata:
  name: configenv
spec:
  containers:
    - name: busybox
      image: busybox:1.27.2
      env:
        - name: TEST_CONFIG
          valueFrom:
            configMapKeyRef:
              name: testconf
              key: test
````

Using all values of `ConfigMap` in `env`:

````yaml
apiVersion: v1
kind: Pod
metadata:
  name: allconfigenv
spec:
  containers:
    - name: busybox
      image: busybox:1.27.2
      envFrom:
      - configMapRef:
          name: testconf
````

Using value of `ConfigMap` in `env`:

````yaml
apiVersion: v1
kind: Pod
metadata:
  name: configvol
spec:
  volumes:
    - name: testconf-volume
      configMap:
        name: testconf
  containers:
    - name: busybox
      image: busybox:1.27.2
      volumeMounts:
        - name: testconf-volume
          mountPath: /etc/testconf
````

## Volumes

### Volume

````yaml
apiVersion: v1
kind: Pod
metadata:
  name: redis
spec:
  containers:
  - name: redis
    image: redis
    volumeMounts:
    - name: redis-storage
      mountPath: /data/redis
  volumes:
  - name: redis-storage
    emptyDir: {}
````

### PersistentVolume

````yaml
apiVersion: v1
kind: Pod
metadata:
  name: test-pd
spec:
  containers:
  - image: k8s.gcr.io/test-webserver
    name: test-container
    volumeMounts:
    - mountPath: /test-pd
      name: test-volume
  volumes:
  - name: test-volume
    gcePersistentDisk:
      pdName: my-data-disk
      fsType: ext4
````

## Deployments

````yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
  labels:
    app: nginx
spec:
  replicas: 1
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:1.7.9
        ports:
        - containerPort: 80
````

## Services

### ClusterIP

Only accesible inside cluster. Is the default value.

````yaml
apiVersion: v1
kind: Service
metadata:  
  name: my-internal-nginx-service
spec:
  selector:    
    app: nginx
  type: ClusterIP
  ports:  
  - name: http
    port: 80
    targetPort: 80
    protocol: TCP
````

### NodePort

Used to configure `Ingress`.

````yaml
apiVersion: v1
kind: Service
metadata:  
  name: nginx-node-service
spec:
  selector:    
    app: nginx
  type: NodePort
  ports:  
  - name: http
    port: 80
    targetPort: 80
    protocol: TCP
````

### Load Balancer

The big downside is that each service you expose with a LoadBalancer will get its own IP address, and you have to pay for a LoadBalancer per exposed service, which can get expensive!

````yaml
apiVersion: v1
kind: Service
metadata:
  name: nginx-service
spec:
  selector:
    app: nginx
  ports:
    - port: 80
      targetPort: 80
  type: LoadBalancer
````

### ExternalName

Used to configure external services that have a URI.

````yaml
apiVersion: v1
kind: Service
metadata:
  name: my-service
  namespace: prod
spec:
  type: ExternalName
  externalName: my.database.example.com
````

### External service with IP

````yaml
kind: Service
apiVersion: v1
metadata:
 name: mongo
Spec:
 type: ClusterIP
 ports:
 - port: 27017
   targetPort: 27017 # can be another port
````

````yaml
kind: Endpoints
apiVersion: v1
metadata:
 name: mongo
subsets:
 - addresses:
     - ip: 10.240.0.4
   ports:
     - port: 27017 # can be another port
````

## ServiceAccount

Processes in containers inside pods can also contact the apiserver. When they do, they are authenticated as a particular Service Account (for example, default).

````yaml
apiVersion: v1
kind: ServiceAccount
metadata:
  name: myapp-sa
  labels:
    account: myapp
````

## Ingress

It sits in front of multiple services and act as a "smart router" or entrypoint into your cluster.

### Single service

````yaml
apiVersion: networking.k8s.io/v1beta1
kind: Ingress
metadata:
  name: test-ingress
  annotations:
    ingress.kubernetes.io/rewrite-target: /
spec:
  backend:
    serviceName: nginx-node-service
    servicePort: 80
````

### Simple fanout

````yaml
apiVersion: networking.k8s.io/v1beta1
kind: Ingress
metadata:
  name: simple-fanout-example
  annotations:
    ingress.kubernetes.io/rewrite-target: /
spec:
  rules:
  - host: foo.bar.com
    http:
      paths:
      - path: /foo
        backend:
          serviceName: service1
          servicePort: 4200
      - path: /bar
        backend:
          serviceName: service2
          servicePort: 8080
````

### Name based virtual hosting

````yaml
apiVersion: networking.k8s.io/v1beta1
kind: Ingress
metadata:
  name: name-virtual-host-ingress
spec:
  rules:
  - host: foo.bar.com
    http:
      paths:
      - backend:
          serviceName: service1
          servicePort: 80
  - host: bar.foo.com
    http:
      paths:
      - backend:
          serviceName: service2
          servicePort: 80
````

````yaml
apiVersion: networking.k8s.io/v1beta1
kind: Ingress
metadata:
  name: name-virtual-host-ingress
spec:
  rules:
  - host: first.bar.com
    http:
      paths:
      - backend:
          serviceName: service1
          servicePort: 80
  - host: second.foo.com
    http:
      paths:
      - backend:
          serviceName: service2
          servicePort: 80
  - http:
      paths:
      - backend:
          serviceName: service3
          servicePort: 80
````

## NetworkPolicy

````yaml
apiVersion: networking.k8s.io/v1                            
kind: NetworkPolicy                                         
metadata:                                                   
  name: demo-np                                             
  namespace: default                                        
spec:                                                       
  podSelector:                                              
    matchLabels:                                            
     app: foo                                               
  policyTypes:                                              
    - Ingress                                               
  ingress:                                                  
    - from:                                                 
        - ipBlock:                                          
            cidr: 192.168.101.0/24                          
        - podSelector:                                      
            matchLabels:                                    
              app: foo                                      
      ports:                                                
        - protocol: TCP                                     
          port: 80                                          
````

## Learn

https://k8s.af/

https://devopswithkubernetes.com/

## Tools

https://k8slens.dev/

## Configure credentials

````
echo -n "{REGISTRY_USERNAME}:{REGISTRY_PASSWORD}" | base64
````

````
{
    "auths": {
        "https://registry.gitlab.com":{
            "auth":"USER_PASS_B64"
        }
    }
}
````

````
apiVersion: v1
kind: Secret
metadata:
  name: registry-credentials
  namespace: dev
type: kubernetes.io/dockerconfigjson
data:
  .dockerconfigjson: BASE_64_ENCODED_DOCKER_FILE

apiVersion: v1
kind: ServiceAccount
metadata:
  name: default
  namespace: dev
imagePullSecrets:
- name: registry-credentials
````

## Top command

````
kubectl apply -f https://github.com/kubernetes-sigs/metrics-server/releases/latest/download/components.yaml
kubectl top pods
Add - --kubelet-insecure-tls to metrics-server image
````

# Old

Share information from pod to container

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: kubernetes-downwardapi-volume-example
  labels:
    zone: us-est-coast
    cluster: test-cluster1
    rack: rack-22
  annotations:
    build: two
    builder: john-doe
spec:
  containers:
    - name: client-container
      image: k8s.gcr.io/busybox
      command: ["sh", "-c"]
      args:
      - while true; do
          if [[ -e /etc/podinfo/labels ]]; then
            echo -en '\n\n'; cat /etc/podinfo/labels; fi;
          if [[ -e /etc/podinfo/annotations ]]; then
            echo -en '\n\n'; cat /etc/podinfo/annotations; fi;
          sleep 5;
        done;
      volumeMounts:
        - name: podinfo
          mountPath: /etc/podinfo
          readOnly: false
  volumes:
    - name: podinfo
      downwardAPI:
        items:
          - path: "labels"
            fieldRef:
              fieldPath: metadata.labels
          - path: "annotations"
            fieldRef:
              fieldPath: metadata.annotations
```

Lifecycle events

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: lifecycle-demo
spec:
  containers:
  - name: lifecycle-demo-container
    image: nginx
    lifecycle:
      postStart:
        exec:
          command: ["/bin/sh", "-c", "echo Hello from the postStart handler > /usr/share/message"]
      preStop:
        exec:
          command: ["/usr/sbin/nginx","-s","quit"]
```

Select node to deploy pod

```yaml
kubectl get nodes 
kubectl label nodes <nodename> disktype=ssd
kubectl get nodes --show-labels
nano dev-pod.yaml

apiVersion: v1
kind: Pod
metadata:
  name: nginx
  labels:
    env: test
spec:
  containers:
  - name: nginx
    image: nginx
    imagePullPolicy: IfNotPresent
  nodeSelector:
    disktype: ssd
```

Taints

```
kubectl get nodes
kubectl taint nodes (nodename) env=dev:NoSchedule
kubectl run nginx —image=nginx
kubectl label deployments/nginx env=dev
kubectl scale deployments/nginx —replicas=5
kubectl get pods -o wide
```

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
  labels:
    app: nginx
spec:
  replicas: 7
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:1.7.9
        ports:
        - containerPort: 80
      tolerations:
      - key: “dev”
        operator: “Equal”
        value: “env”
        effect: “NoSchedule”
```



```
A node selector affects a single pod template, asking the scheduler to place it on a set of nodes. A NoSchedule taint affects all pods asking the scheduler to block all pods from being scheduled there.

A node selector is useful when the pod needs something from the node. For example, requesting a node that has a GPU. A node taint is useful when the node needs to be reserved for special workloads. For example, a node that should only be running pods that will use the GPU (so the GPU node isn't filled with pods that aren't using it).

Sometimes they are useful together as in the example above, too. You want the node to only have pods that use the GPU, and you want the pod that needs a GPU to be scheduled to a GPU node. In that case you may want to taint the node with dedicated=gpu:NoSchedule and add both a taint toleration and node selector to the pod template.
```

## 