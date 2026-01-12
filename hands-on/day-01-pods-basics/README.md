I have started learning Kubernetes as a DevOps fresher and my main focus is to learn by doing.
Instead of just reading theory, I am practicing hands-on and trying to understand why each command is used.

To avoid installation issues on my local system, I used the KillerKoda Kubernetes Playground.
It gives a ready-made Kubernetes cluster in the browser, so I could directly focus on learning Kubernetes.

Today, this is what I practiced step by step:

• Connected to a Kubernetes cluster
• Checked Nodes and Pods
• Created my first Pod using a command
• Inspected Pod details
• Created a Pod using YAML (real DevOps way)
• Deleted the Pod to understand reproducible infrastructure
• Checked application logs
• Entered inside the container using exec

First, I checked whether kubectl was installed and connected properly.

$ kubectl version

Why I used this:
This helped me confirm that kubectl is available and connected to the Kubernetes cluster.

Simple way to think:
Like checking if the car key works before starting the car.

Then, I checked if the Kubernetes cluster was actually running.

$ kubectl cluster-info

Why I used this:
To make sure the Kubernetes control plane is up and the cluster is ready to accept commands.

Simple way to think:
Checking if the city office is open.

After that, I checked the Nodes in the cluster.

$ kubectl get nodes

Why I used this:
Nodes are the machines (VMs or servers) where applications run.
If the node status is Ready, it means Kubernetes can run Pods on it.

Simple way to think:
Buildings that are ready to open shops.

Next, I checked if any Pods were already running.

$ kubectl get pods

Why I used this:
To see what applications are already running in the cluster.
No Pods were running, which confirmed that the environment was clean.

Simple way to think:
Checking which shops are already open.

Then I created my first Pod.

$ kubectl run nginx-pod --image=nginx

Why I used this:
This command quickly creates a Pod using the nginx image.
Kubernetes automatically pulls the image, decides where to run it, and starts the container.

Simple way to think:
Telling the system to open one shop automatically.

After creating the Pod, I checked its status.

$ kubectl get pods

Why I used this:
To confirm that the Pod is created and running successfully.

Next, I inspected the Pod in detail.

$ kubectl describe pod nginx-pod

Why I used this:
This shows detailed information like which Node the Pod is running on, container details, and events.
This command is very useful when something goes wrong.

Simple way to think:
Looking at a full shop report including location and activity.

After that, I created a Pod using YAML, which is how things are done in real DevOps projects.

The pod.yaml file I used:

apiVersion: v1
kind: Pod
metadata:
name: my-first-yaml-pod
spec:
containers:

name: nginx-container
image: nginx

Why YAML:
YAML lets us define what we want, and Kubernetes handles how to do it.
This makes everything reusable and easy to manage using Git.

Simple way to think:
Giving written instructions instead of verbal ones.

Then I applied the YAML file.

$ kubectl apply -f pod.yaml

Why I used this:
This creates the Pod using the YAML file.
This is the preferred and real-world way of deploying things in Kubernetes.

I checked the Pods again.

$ kubectl get pods

Why I used this:
To confirm that the Pod created using YAML is running properly.

Then I inspected the YAML-created Pod.

$ kubectl describe pod my-first-yaml-pod

Why I used this:
To check Node assignment, container status, and events.

After that, I deleted the Pod.

$ kubectl delete pod my-first-yaml-pod

Why I used this:
In Kubernetes, Pods are temporary and can be recreated anytime using YAML.
Deleting Pods helps build the DevOps mindset of reproducible infrastructure.

Simple way to think:
Closing a shop because you can open it again anytime using the same plan.

Next, I checked application logs.

$ kubectl logs nginx-pod

Why I used this:
Logs help understand what the application is doing and are the first thing to check during debugging.

Simple way to think:
Checking CCTV or activity logs.

Finally, I entered inside the running container.

$ kubectl exec -it nginx-pod -- /bin/bash

Why I used this:
This allows direct access inside the container to check files or processes.
It is helpful for troubleshooting in real environments.

Inside the container, I ran:
ls
exit
