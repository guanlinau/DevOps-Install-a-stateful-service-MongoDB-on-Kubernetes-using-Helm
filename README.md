### Install a stateful service (MongoDB) on Kubernetes using Helm

### Technologies Used:

K8s, Helm, MongoDB, Mongo Express, Linode LKE, Linux

### Project Description:

1-Create a managed K8s cluster with Linode Kubernetes Engine

2-Deploy replicated MongoDB service in LKE cluster using a Helm chart

3-Configure data persistence for MongoDB with Linode’s cloud storage

4-Deploy UI client Mongo Express for MongoDB

5-Deploy and configure nginx ingress to access the UI application from browser

### Instructions:

###### Step 1: Create some accounts and install helm

1- Create an account in Linode

2- Create an account in Helm club

3- Install helm via brew

###### Step 2: Create a cluster on Linode with two worker node

###### Step 3: Export cluster config file as env variable for providing credentials and certificate

```
export KUBCONFIG=test-kubeconfig.yaml
```

```
kubectl get node
```

###### Step 4: Deploy mongodb as a statefulset via helm chart

1- add mongodb helm chart repo into cluster

```
helm repo add my-repo https://charts.bitnami.com/bitnami
```

2-create values.yaml file to overwrite default values

```
architecture: replicaset
replicaCount: 3
persistence:
    storageClass: "linode-block-storage"
auth:
    rootPassword: secret-root-pwd

```

3-Create mongodb statefulset

```
helm install mongob --value test-mongodb-values.yaml bitnami/mongodb
```

###### Step 5: Deploy mongodb express as a deployment via mongo-express.yaml file

1-create mongo-express.yaml deployment and service file

2-create mongo-express deployment and service components

```
kubectl apply -f mongo-express.yaml
```

###### Step 6: Install Ingress controller-nginx-ingress controller via helm chart

![image](image/Screenshot%202023-03-08%20at%2012.34.51%20am.png)

###### Step 7: Configure and create ingress role for mongo-express

```
kubectl apply -f test-ingress.yaml
```

###### Step 8: open host name in the browser

```
nb-139-162-140-213.frankfurt.nodebalancer.linode.com
```
