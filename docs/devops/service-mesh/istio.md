# Istio

## Install

- Download zip
- Unzip and move to folder
- Add bin to PATH

## Commands

Install

````
istioctl install --set profile=demo
````

Show pods

````
kubectl get pods -n istio-system
````

Uninstall 

````
istioctl x uninstall --purge
kubectl delete namespace istio-system
````

Enable injection

````
kubectl label namespace default istio-injection=enabled
````

## Sample app components

### Service

````yaml
apiVersion: v1
kind: Service
metadata:
  name: myapp
  labels:
    app: myapp
    service: myapp
spec:
  ports:
  - port: 9080
    name: http
  selector:
    app: myapp
````

Remember that default type is `ClusterIP`

### ServiceAccount

````yaml
apiVersion: v1
kind: ServiceAccount
metadata:
  name: myapp-sa
  labels:
    account: myapp
````

### Deployment

````yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: myapp-v1
  labels:
    app: myapp
    version: v1
spec:
  replicas: 1
  selector:
    matchLabels:
      app: myapp
      version: v1
  template:
    metadata:
      labels:
        app: myapp
        version: v1
    spec:
      serviceAccountName: myapp-sa
      containers:
      - name: myapp
        image: myapp-image-url
        imagePullPolicy: IfNotPresent
        ports:
        - containerPort: 9080
````

## Networking components

### Gateway

A `Gateway` configures a load balancer for HTTP/TCP traffic, regardless of where it will be running. Any number of gateways can exist within the mesh and multiple different gateway implementations can co-exist.

````yaml
apiVersion: networking.istio.io/v1alpha3
kind: Gateway
metadata:
  name: my-gateway
spec:
  selector:
    istio: ingressgateway # use istio default controller
  servers:
  - port:
      number: 80
      name: http
      protocol: HTTP
    hosts:
    - "*"
````

`hosts`can be a list of allowed hosts (for example `myhost.com`) or `*` for any.

### VirtualService

A `VirtualService` describes the mapping between one or more user-addressable destinations to the actual destination workloads inside the mesh.

````yaml
apiVersion: networking.istio.io/v1alpha3
kind: VirtualService
metadata:
  name: my-service
spec:
  hosts:
  - "*"
  gateways:
  - my-gateway
  http:
  - match:
    - uri:
        exact: /test
    - uri:
        prefix: /myapp/v1
    route:
      - destination:
        host: myapp
        subset: v1
        port:
          number: 9080
  - match:
    - uri:
      prefix: /myapp/v2
    route:
      - destination:
        host: myapp
        subset: v2
````

`hosts` : The destination hosts to which traffic is being sent.

We can configure weigths

````yaml
spec:
  hosts:
  - reviews
  http:
  - route:
    - destination:
        host: reviews
        subset: v1
      weight: 75
    - destination:
        host: reviews
        subset: v2
      weight: 25
````

### DestinationRule

If we use `subset`in the `VirtualService` we need to define the `DestinationRule`

````yaml
apiVersion: networking.istio.io/v1alpha3
kind: DestinationRule
metadata:
  name: my-destination-rule
spec:
  host: myapp # myapp.default.svc.cluster.local
  trafficPolicy:
    loadBalancer:
      simple: RANDOM
  subsets:
  - name: v1
    labels:
      version: v1
  - name: v2
    labels:
      version: v2
    trafficPolicy:
      loadBalancer:
        simple: ROUND_ROBIN
  - name: v3
    labels:
      version: v3
````

### Sidecar

By default, Istio configures every Envoy proxy to accept traffic on all the ports of its associated workload, and to reach every workload in the mesh when forwarding traffic. You can use a sidecar configuration to do the following:

- Fine-tune the set of ports and protocols that an Envoy proxy accepts.
- Limit the set of services that the Envoy proxy can reach.