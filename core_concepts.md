# prereq

    alias k8 kubectl

# Pods

## Create
    
    kubeclt create -f ./pod.yaml

## edit

# cluster info

    k8 cluster-info

# ReplicationController

## Create

    k8 create -f rc-definition.yml

## Scale

    k8 scale --replicas 4 -f rc-definition.yml

    k8 scale --replicas 4 replicaset frame
    
## Update

    k8 replace -f rc-definition.yml


# ReplicaSet

Alles van Replicasets werkt. Grootste verschil is dat de definition.yml een veld 'selector' moet hebben

# Deployment

Superset of replicaset (resuse definition file)

Meer info (ander formaat):

    k8 get pods --output wide|json|name|yaml

# Namespaces

connect to pod in different namespace: 

    service.namespace.svc.cluster.local

create using command: 

    k8 create .. --namespace=dev

switch to another namespace 

    k8 config set (k8 config current-context) --namespace=dev

# Quota

