# Central observability w/ cilium mesh and prometheus/agent

## Prereq's
```
Cilium mesh requires the kubernetes service cidr not to conflict.
in the example we will use 10.0.0.0/8 for cluster 1 and 10.1.0.0/8 for cluster 2
This also assumes cluster 1's ips are 10.0.3.1 and 10.0.3.2

cluster 2's ips are 10.3.2.1 10.3.2.1

This functions in a flat or not flat network architecture.
```
## Cilium helm values
---
Notable cilium helm values
clustermesh enabled true
cluster names and id's (can't be 0)
hubble-relay rollout restart pods true
clustermesh pre config line xxx
```
