# Kuma

## Install

````bash
curl -L https://kuma.io/installer.sh | sh -
PATH=$PATH:~/kuma-0.7.1/bin
````

## Comands

Install contrlo plane

````
kumactl install control-plane | kubectl apply -f -
````

Open dashboard

````
kubectl port-forward svc/kuma-control-plane -n kuma-system 5681:5681
````

http://127.0.0.1:5681/gui

Install metrics

````
kumactl install metrics | kubectl apply -f -
````

Open metrics

````
kubectl port-forward svc/grafana -n kuma-metrics 3000:80
````

http://127.0.0.1:3000/







````
echo "apiVersion: kuma.io/v1alpha1
kind: Mesh
metadata:
  name: default
spec:
  mtls:
    enabledBackend: ca-1
    backends:
    - name: ca-1
      type: builtin" | kubectl apply -f -
````



````
echo "apiVersion: kuma.io/v1alpha1
kind: TrafficPermission
mesh: default
metadata:
  namespace: default
  name: all-traffic-allowed
spec:
  sources:
    - match:
        kuma.io/service: '*'
  destinations:
    - match:
        kuma.io/service: '*'" | kubectl apply -f -
````

````
echo "apiVersion: kuma.io/v1alpha1
kind: Mesh
metadata:
  name: default
spec:
  mtls:
    enabledBackend: ca-1
    backends:
    - name: ca-1
      type: builtin
  metrics:
    enabledBackend: prometheus-1
    backends:
    - name: prometheus-1
      type: prometheus" | kubectl apply -f -
````

