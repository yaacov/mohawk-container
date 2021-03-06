# Run on Kubernetes and OpenShift
This directory include instructions and templates for building container pods that will scrape data from kubernetes and openshift into a mohawk server, the openshift setup will also integrate the Mohawk metrics into Openshift UI console.

#### On OpenShift:
```
wget https://raw.githubusercontent.com/yaacov/mohawk-container/master/container-metrics/setup.sh

oc project kube-system

# run setup script
# ROUTER_IP is the IP address of the compute node running the haproxy.
# e.g. ROUTER_IP=10.123.0.34 bash ./setup.sh
ROUTER_IP=<ip of mohawk route> bash ./setup.sh
```

#### On Kubernetes:

```
# Add cluster admin role to system:anonymous
kubectl create clusterrolebinding kube-system-cluster-admin \
        --user system:serviceaccount:kube-system:default --clusterrole cluster-admin
kubectl create clusterrolebinding kube-system-cluster-admin \
        --user system:anonymous --clusterrole cluster-admin

# Get and run template
wget https://raw.githubusercontent.com/yaacov/mohawk-container/master/container-metrics/mohawk-k8s.yaml
kubectl create -f Projects/mohawk-container/mohawk-k8s.yaml

```
