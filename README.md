# Central observability w/ cilium mesh and prometheus/agent

## Prereq's
```
Cilium mesh requires the kubernetes service cidr not to conflict.
in the example we will use 10.0.0.0/8 for cluster 1 and 10.1.0.0/8 for cluster 2
This also assumes Central Cluster ip is 192.10.1.2

Dev cluster is 192.10.1.3

This functions in a flat or not flat network architecture.
```
## Notable Cilium helm values
```
Notable cilium helm values
clustermesh enabled true
cluster names and id's (can't be 0)
hubble-relay rollout restart pods true
clustermesh pre config line xxx
cluster authmode: cluster
kube-proxy enabled
l7 proxy enabled
```
## Notable Prometheus manifest values
```
enableRemoteWriteReceiver: true

I've set these though I haven't found them that important
  externalLabels:
    cluster: "promcentral"
  replicaExternalLabelName: "promcentral"
```

## Notable prometheus service manifest value
```
Expose the service to the mesh
add annotations
  annotations:
    service.cilium.io/global: "true"
```

## Example service monitor for central cluster
```
relabelings replacement to cluster name.

Many grafana charts have cluster/multi cluster capabilities, w/o this relabiling the central cluster cannot showcase it's own metrics
```

## notable prometheus agent values
```
remote write and external labels

With this cluster no relabelings are required as all external labels are transmitted appropriately
```

## Notable decoy prometheus on "agent" cluster values
```
replicas = 0
Using this just to autogenerate the service so that the service is the same amongst all clusters and can be globally routed througout cilium mesh
```

## prometheus agent service values
```
global annotation for cilium
```
