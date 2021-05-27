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