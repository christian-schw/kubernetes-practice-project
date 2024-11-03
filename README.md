# Understanding ConfigMaps, DaemonSets, Kubernetes Services, Secrets & Persistent Volume Claims
This repository was created as part of IBM's "Introduction to Containers, Kubernetes and OpenShift" course.<br>
It's a practice project about Kubernetes using Docker.<br>
Much of the code was cloned from the IBM repository: https://github.com/ibm-developer-skills-network/containers-project.git<br>
<br>
<br>



## Course Information
Title: Introduction to Containers, Kubernetes and OpenShift<br>
Type: Practice Project<br>
Course Provider: IBM<br>
<br>
<br>



## Information about the Project
### General
- Client: Myself
- Project Goal: Build and deploy an application to Kubernetes, then understand and create ConfigMaps, DaemonSets, Kubernetes Services, Secrets, and further explore Volumes & Persistent Volume Claims.
- Number of Project Participants: 1 (Cloned repository of IBM. Developed the rest on my own)
- Time Period: November, 2024
- Industry / Area: DevOps
- Role: Developer
- Languages: English
- Result: Application successfully built and deployed. Improved understanding of several objects in Kubernetes.
<br>

### Tech Stack
With regard to my role:
- Containerization Tool: Docker
- Container Registry: IBM Cloud Container Registry
- IBM Cloud IDE (based on Theia and Container)
- Container Orchestration Tool: Kubernetes
<br>
<br>



## What I have done as part of the project
As a lot of the work was done in the terminal, it is not visible in the repository.<br>
I therefore explain my completed tasks in the project.<br>
<br>

### Build and deploy the application to Kubernetes
Setup of the environment variable namespace (user name is already predefined in IBM Cloud IDE):<br>
TODO: Insert image setup env var<br>
<br>
The image was then built using the Dockerfile.<br>

```
docker build . -t us.icr.io/$MY_NAMESPACE/myapp:v1
```

The -t flag was used to set the name and tag of the image according to the IBM course naming convention.<br>
Result:<br>
TODO: Insert image docker images<br>

After the image has been built, it is pushed into the IBM Container Registry:<br>

```
docker push us.icr.io/$MY_NAMESPACE/myapp:v1 
```

Result:<br>
TODO: Insert image cr images<br>

The K8s object deployment is then created.<br>
Here the placeholder of the namespace must be replaced with my namespace:<br>
TODO: Insert image deployment.yaml<br>

Apply the deployment:<br>

```
kubectl apply -f deployment.yml
```

Verification of the deployment:<br>
TODO: Insert image pods<br>

Now start application on port-forward:<br>

```
kubectl port-forward deployment.apps/myapp 3000:3000 
```

Port forwarding in Kubernetes is a mechanism that allows you to access services running within a Kubernetes cluster from your local machine or another external system.<br>
It's useful for debugging, testing, and accessing services during development.<br>
<br>
Output of application:<br>
TOOD: Insert image application output<br>
<br>

### Set up a ConfigMap
To decouple environment-specific configuration from the container image, so that the application is easily portable.<br>
According to the task, literals are to be used in the practical project.<br>
These are defined with the flag '--from-literal'.<br>
This makes it possible to create a ConfigMap via CLI.<br>
<br>
Two environment variables should be created:<br>
- Key: server-url, Value: http://example.com
- Key: timeout, Value: 5000
<br>
This results in the following command:<br>

```
kubectl create configmap myapp-config --from-literal=server-url=http://example.com --from-literal=timeout=5000
```

Verification of the ConfigMap:<br>
TODO: Insert image env var configmap<br>
Data = 2, which means that two environment variables have been created. Everything fits.<br>
<br>

### Create a DaemonSet
DaemonSet is used to ensure that a pod runs on each node in the cluster, including the nodes where the application pods are deployed.<br>
Result: Enhanced availability and fault tolerance of the application through redundancy and load distribution.<br>
<br>
First, the daemonset.yaml file is adjusted.<br>
Here the placeholder of the namespace must be replaced with my namespace:<br>
TODO: Insert image adjustment daemonset yaml<br>

Next, the daemonset.yaml file is applied:<br>
```
kubectl apply -f daemonset.yaml
```

Verification of the DaemonSet:<br>
TODO: Insert image verification daemonset<br>
<br>

### Expose application within the cluster
TODOO<br>
<br>

### Create and manage secrets
TODOO<br>
<br>

### Provide storage for application
TODOO<br>
<br>
<br>



## Getting Started
The code was only executable with the help of the IBM Cloud IDE.<br>
The IDE had many necessary tools and accesses preconfigured. These include, for example, Kubernetes installation or IBM Cloud Container Registry.
<br>
<br>



## Contact
If you have any questions, please feel free to reach out via email: christian-schwanse (at) gmx.net