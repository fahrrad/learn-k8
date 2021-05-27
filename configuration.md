# Docker

    docker run ubuntu

Stops immediately: does not run a OS (just runs the app). Container exists if process stops. (bash stops if it does not find a terminal)

    docker run sleep 5

Overrides the CMD from the Dockerfile

    CMD sleep 5
    CMD ["sleep", "4"]

    ENTRYPOINT ["sleep"]
    CMD ["5"]  // default
    docker run sleeper 10

In yaml file: ENTRYPOINT is overridden by command en CMD is overridden by args

# Config

## configMap

### create 

    k8 create -f config-map.yml

### refernce 1 value

    env:
        - name: APP_COLOR
          valueFrom:
            configMapKeyRef:
                name: configmap
                key: APP_COLOR

### full configmap

    envFrom:
        - configMapRef:
            name: configmap

## Secrets

Have to be added base64 encoded: 

    echo -n "secret" | base64

Voorbeeld in pod definition

# Security

    containers:
        securityContext:
            runAsUser: 1000
            capabilities:
                add: ["MAC_ADMIN"]


# Service Accounts

kunnen gebruikt worden om de K8 API te queryen. 

Een nieuwe service account kan gemaakt worden

    k8 create serviceaccount dashboard-sa

dan kan die in een pod gebruikt worden door

        serviceAccount: dashboard-sa

dit zorgt ervoor dat een directory gemounted wordt (standaard onder /var/run/secrets/kubernetes.io/serviceaccount) met een token

```
    # Point to the internal API server hostname
    APISERVER=https://kubernetes.default.svc

    # Path to ServiceAccount token
    SERVICEACCOUNT=/var/run/secrets/kubernetes.io/serviceaccount

    # Read this Pod's namespace
    NAMESPACE=$(cat ${SERVICEACCOUNT}/namespace)

    # Read the ServiceAccount bearer token
    TOKEN=$(cat ${SERVICEACCOUNT}/token)

    # Reference the internal certificate authority (CA)
    CACERT=${SERVICEACCOUNT}/ca.crt

    # Explore the API with TOKEN
    curl --cacert ${CACERT} --header "Authorization: Bearer ${TOKEN}" -X GET ${APISERVER}/api

```

