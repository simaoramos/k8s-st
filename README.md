# Studying Kubernetes

## Known kubectl commands

### List

#### > kubectl get all
It will list all the objects in the nodes like deployments, replicasets and pods.

#### > kubectl get <pods|replicasets|replicationcontrollers|deployments>
It will list all the objects in the nodes by the given type. Also it is possible to filter its name e.g. kubectl get pod redis

#### > kubectl get <pods|replicasets|replicationcontrollers|deployments> -o wide
Has the same purpose of the above but gives us more detailed information.

#### > kubectl describe <pods|replicasets|replicationcontrollers|deployments> object_name
Shows all the detailed information about a single object: metadata, containers, conditions, volumes and event logs.

### Create/Run

#### > kubectl run pod_name --image=image_name
Creates and runs a new pod with the given image.

#### > kubectl run pod_name --image=image_name --dry-run=client -o yaml > pod-definition.yaml
This won't run the pod, instead it will create a new configuration file with the given image and file name.

#### > kubectl create -f rc-definition.yml
Creates and runs a new object (pod|replicaset|replicationcontrollers|etc) from a given configuration file.

#### > kubectl apply -f pod-definition.yml
Creates/updates and runs a new object (pod|replicaset|replicationcontrollers|etc) from a given configuration file. If used to update a running object, it will trigger a rollout on the running pods.

#### > kubectl create deployment dep-name --image=image_name
Creates a new deployment with the given name and image.

### Edit

#### > kubectl edit <pods|replicasets|replicationcontrollers|deployments> object_name
Edits the configuration of an existing running object. Changes made here will be directly applied on the running configuration as soon as is saved. 

#### > kubectl replace -f rs-definition.yml
Replaces the configuration of the object based on the given file. For example, it could be a way to change the replicas to scale an application.

#### > kubectl scale --replicas=6 -f rs-definition.yml
Changes the number of replicas given a existing configuration file. This will NOT change the number of replicas in the file it will just edit the running replicaset.

#### > kubectl scale replicaset myapp-rs --replicas=6
Changes the number of replicas given the name of the replicaset.

### Delete

#### > kubectl delete <pods|replicasets|replicationcontrollers|deployments> object_name
Deletes a single object by its name.

#### > kubectl delete <pods|replicasets|replicationcontrollers|deployments> --all
Deletes all objects by the given type.

#### > kubectl delete <pods|replicasets|replicationcontrollers|deployments> -l app=myapp
Deletes all objects by the given type matching the given label.

### Rollout deployments

#### > kubectl create -f deployment-definition.yml --record
This will create a new deployment for the given configuration file. The record flag (deprecated) will indicate that we want to record the change cause.

#### > kubectl apply -f deployment-definition.yml --record
This will create/update a deployment for the given configuration file. The record flag (deprecated) will indicate that we want to record the change cause.

#### > kubectl set image deployments/deployment-name container-name=image-name --record
Updates the running deployment's image. This does NOT update the configuration file. The record flag (deprecated) will indicate that we want to record the change cause.

#### > kubectl rollout status deployments/deployment-name
This will show the rollout status of a deployment by its name.

#### > kubectl rollout history deployments/deployment-name
This will show the rollout history of the last deployment by its name.

#### > kubectl rollout undo deployments/deployment-name
This will rollback the previous deployment by the given name.

#### > kubectl expose deployment deployment-name --name=service-name --target-port=8080 --type=NodePort --port=8080 --dry-run=client -o yaml > svc-definition.yml
This will create a service definition file (since using dry-run=client parameter) named svc-definition.yml with the given type (NodePort) and ports.