# K8sContainerRequests

Next steps: 

Use ACM policy, something like:

```
apiVersion: policy.open-cluster-management.io/v1
kind: Policy
metadata:
  name: policy-container-requests
spec:
  policy-templates:
    - objectDefinition:
        apiVersion: templates.gatekeeper.sh/v1beta1
        kind: ConstraintTemplate
        metadata:
          name: k8scontainerrequests
        spec:
        ...
    - objectDefinition:
        apiVersion: constraints.gatekeeper.sh/v1beta1
        kind: K8sContainerRequests
        metadata:
          name: container-must-have-requests
        spec:
        ...
---
apiVersion: policy.open-cluster-management.io/v1
kind: PlacementBinding
metadata:
  name: binding-policy-container-requests
placementRef:
  name: placement-policy-gatekeeper
  kind: Placement
  apiGroup: cluster.open-cluster-management.io
subjects:
- name: policy-container-requests
  kind: Policy
  apiGroup: policy.open-cluster-management.io
---
apiVersion: cluster.open-cluster-management.io/v1
kind: Placement
metadata:
  name: placement-policy-container-requests
spec:
...
```
