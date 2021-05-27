# Pod Lifecycle

status :
 - pending (scheduler tries to find a node)
 - containercreating  (starting all containers)
 - running

conditions: 
 - PodScheduled
 - initialised
 - containersready
 - ready

# Readiness

see conditions in the `k8 describe pod` output. Only if pods are 'ready' will they receive traffic

    containers:
        readinessProbe:
            httpGet:
                path: /api/ready
                port: 8080


    containers:
        readinessProbe:
            tcpSocket:
                port: 3333
            

    containers:
        exec:
            command:
                - cat
                - /app/is_ready
        initialDelaySecond: wait for x seconding
        periodSeconds: 5
        failureTreshold: 10


# Liveness probe

will restart if failed

    containers:
        livenessProbe:
            tcpSocket:
                port: 3333
            

# Side note: docker

    eval (minikube docker-env)

on local machine sets the docker env to that of minicube, so we can build and upload images

# Logs

    k8 logs -f pod_name [container_name]

# deployments 

create: k8 create -f deployment-definition.yml
get: k8 get deployments
update: k8 apply -f deployment-definition.yml
        k8 set image deployment/my-deployment nginx=nginx:1.8.2

status: k8 rollout status deployment/my-deployment

revision

# Jobs

Not meant to rnu forever (like webserver)

    RestartPolicy: never

CronJobs (apiVersion: )