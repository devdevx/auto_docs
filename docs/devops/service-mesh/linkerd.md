# Linkerd

## Install client

````bash
curl -sL https://run.linkerd.io/install | sh
export PATH=$PATH:$HOME/.linkerd2/bin
linkerd version
````

## Install in cluster

```bash
linkerd check --pre
linkerd install | kubectl apply -f -
linkerd install --proxy-auto-inject | kubectl apply -f -
linkerd check
```

## Access dashboards

```bash
linkerd dashboard &
```

## Adding service to Linkerd

In order for your services to take advantage of Linkerd, they need to be "added to the mesh" by having Linkerd's data plane proxy injected into their pods. This is typically done by annotating the namespace, deployment, or pod with the `linkerd.io/inject: enabled` Kubernetes annotation. This annotation triggers automatic proxy injection when the resources are created.

```bash
kubectl label namespace default linkerd.io/inject=enabled
```

```bash
cat deployment.yml | linkerd inject - | kubectl apply -f -
```



# TODO

https://linkerd.io/2/tasks/exposing-dashboard/

https://linkerd.io/2/tasks/distributed-tracing/

Namespace Injection BUG

Production install

https://blog.intenseye.com/service-mesh-with-linkerd2-part-1/

https://blog.intenseye.com/service-mesh-with-linkerd2-part-2/

https://blog.polymatic.systems/service-mesh-wars-goodbye-istio-b047d9e533c7

