# Tensorboard for Kubernetes

This is a simple setup for running Tensorboard with Kubernetes.

## Quick Start

1. Create PVC
   1. `kubectl apply -f tensorboard-pvc.yml`
2. Create Deployment
   1. `kubectl apply -f tensorboard-deployment.yml`
3. Create Service
   1. `kubectl apply -f tensorboard-service.yml`

You can access your tensorboard instance by port-forwarding your pod from kubernetes to your local system. After port-forwarding you can simply open `localhost:6006` in your browser.

1. `kubectl port-forward tensorboard-REPLACE-HASH 6006:6006`

## Logging

To log new runs to your tensorboard instance you need to mount the tensorboard pvc and log your files to this directory.

```yml
...
volumeMounts:
            - name: tensorboard-persistent-storage
              mountPath: /pv/tensorboard
...
volumes:
    - name: tensorboard-persistent-storage
        persistentVolumeClaim:
        claimName: tensorboard-pvc
...
```