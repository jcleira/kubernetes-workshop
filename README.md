# Vigolabs Kubernetes workshop

This repository contains the support files used @ the [Vigolabs Kubernetes workshop](https://www.meetup.com/es-ES/Vigo-Labs/events/242161923/) on August 9 2017.

![Kubernetes logo](https://web-836ky6sfl9f868egnyg.netdna-ssl.com/cnt/uploads/2017/06/Kubernetes2.png)

The following commands it's the roadmap used during the workshop:

```bash
# Export the following var changing the workshop_number with your id/number.
export KOPS_STATE_STORE=s3://vigolabs-k8s-workshop-(workshop_number)

# Export a name for the cluster changing the workshop_number with your id/number.
export NAME=vigolabs-workshop-(workshop_number).ederium.com

# Create the cluster configuration.
kops create cluster --zones eu-west-1a ${NAME}

# Review the cluster node configuration.
kops edit ig --name=${NAME} nodes

# Review the master node configuration.
kops edit ig --name=${NAME} master-eu-west-1a

# Launch the cluster.
kops update cluster --name=${NAME} --yes

# Validate the cluster
kops validate cluster

# See the running nodes
kubectl get nodes

# See the system running pods.
kubectl get po --all-namespaces

# Create another ssh session with a watch
watch kubectl get po --all-namespaces

# Create the prometheus configuration.
kubectl create -f prometheus-configmap.yaml

# Create the prometheus deployment.
kubectl create -f prometheus-deployment.yaml

# Create the prometheus service.
kubectl create -f prometheus-service.yml

# Create the grafana deployment.
kubectl create -f grafana-deployment.yaml

# Create the grafana service.
kubectl create -f grafana-service.yaml

# Get the AWS Elastic Balancer URL from the prometheus service.
kubectl describe svc prometheus

# Get the AWS Elastic Load Balancer URL from the grafana service.
kubectl describe svc grafana

# Create the oklog daemonset.
kubectl create -f oklog-daemonset.yaml

# oklog query help.
oklog query -h

# oklog query logs.
oklog query -from 1h --store ec2-54-76-214-115.eu-west-1.compute.amazonaws.com

# Create the web application deployment.
kubectl create -f webapp-deployment.yaml

# Create the web application service.
kubectl create -f webapp-service.yaml

# Scale the web application service.
kubectl scale --replicas=10 deployment/sample-web-service

# Update deployment image.
kubectl set image deployment/sample-web-service sample-web-service=jcorral/sample-web-service:v2

# Get the AWS Elastic Load Balancer URL from the webapp service.
curl -v <AWS_BALANCER_URL>/version

# Get the running nodes.
kubectl get nodes

# Get a node into maintenance.
kubectl cordon <node_name>
```
