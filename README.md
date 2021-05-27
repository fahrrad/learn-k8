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

