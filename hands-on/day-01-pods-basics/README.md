# Kubernetes Learning Notes – Day 01 (Hands-On Basics)

This repository documents my Kubernetes learning as a DevOps fresher.
I am focusing on **hands-on practice with clear understanding of why each command is used**.

To avoid local installation complexity, I practiced Kubernetes using the **KillerKoda Kubernetes Playground**, which provides a ready-to-use Kubernetes cluster in the browser.

---

Today I practiced the following:
- Connected to a Kubernetes cluster
- Checked Nodes and Pods
- Created my first Pod using command
- Inspected Pod details
- Created Pod using YAML (real DevOps way)
- Deleted Pod (reproducible infrastructure mindset)
- Checked logs
- Entered container using exec

---

I used the commands below and understood **why each command is important**.

---

kubectl version --short  

Why?  
To confirm that kubectl is installed and connected to the Kubernetes cluster.

Analogy:  
Checking if the car key works before driving.

---

kubectl cluster-info  

Why?  
To verify that the Kubernetes control plane is running and accessible.

Analogy:  
Checking if the city office is open.

---

kubectl get nodes  

Why?  
Nodes are the machines (VMs/servers) where Pods run.  
Status `Ready` means the machine can run applications.

Analogy:  
Buildings that are ready to open shops.

---

kubectl get pods  

Why?  
To check which applications (Pods) are currently running in the cluster.  
Initially, no Pods were running, which confirmed a clean environment.

Analogy:  
Checking which shops are open in the city.

---

kubectl run nginx-pod --image=nginx  

Why?  
To quickly create a Pod for practice using the nginx image.  
Kubernetes automatically pulls the image, creates the Pod, assigns it to a Node, and starts the container.

Analogy:  
Telling the city system to open one shop automatically.

---

kubectl get pods  

Why?  
To confirm that the Pod was created successfully and is in `Running` state.

---

kubectl describe pod nginx-pod  

Why?  
To view detailed information about the Pod such as:
- Which Node it is running on
- Container details
- Events and errors (if any)

This command is very important for troubleshooting.

Analogy:  
Viewing a full shop report including location and activity log.

---

I then created a Pod using YAML, which is the **real DevOps approach**.

pod.yaml file used:

apiVersion: v1  
kind: Pod  
metadata:  
  name: my-first-yaml-pod  
spec:  
  containers:  
  - name: nginx-container  
    image: nginx  

Why YAML?  
YAML allows declarative configuration where we tell Kubernetes **what we want**, and Kubernetes handles **how to do it**.  
This makes infrastructure reproducible and version-controlled using Git.

Analogy:  
Submitting a written form instead of giving verbal instructions.

---

kubectl apply -f pod.yaml  

Why?  
To create the Pod from the YAML file.  
This is the preferred command used in real production environments.

---

kubectl get pods  

Why?  
To confirm that the Pod created using YAML is running successfully.

---

kubectl describe pod my-first-yaml-pod  

Why?  
To verify Node assignment, container status, and events for the YAML-created Pod.

---

kubectl delete pod my-first-yaml-pod  

Why?  
Pods can be deleted safely because they can be recreated anytime from YAML.  
This helps build the DevOps mindset that infrastructure is temporary and reproducible.

Analogy:  
Closing a shop because you can reopen it anytime using the same plan.

---

kubectl logs nginx-pod  

Why?  
To view application logs.  
This is the first step when debugging application issues.

Analogy:  
Checking CCTV or activity register of a shop.

---

kubectl exec -it nginx-pod -- /bin/bash  

Why?  
To enter inside the running container and inspect files or processes.  
This is useful for troubleshooting in real environments.

Inside the container I used:
ls  
exit  

---

What I learned today:
- Kubernetes manages containers automatically
- Pod is the smallest deployable unit
- Node is the machine where Pods run
- kubectl get and describe are core commands
- YAML is the real DevOps way of working
- Logs and exec are essential for debugging

---

Next step:
Learning Deployments, ReplicaSets, and self-healing in Kubernetes.
