# High level description of how my test stratergy would look for feature requirement 9:

Given that the app back-end has been deployed to a Kurbernetes 3 node cluster which has multiple replicas of each pod.

## 1. Ensuring redundency within the cluster:

- I would initially want to make sure that the redundency of the 3 node cluster's are infact in place and running as expected. 

- Something I would want to specifically check is if the cluster has at least has a second or	even third control plane node in place, in case an application node of the cluster were to go down, so would a control plane instance.
These are effected when nodes go down and this is critical to the requirement of cluster and remaining nodes up and running when a node goes down. The tester could make use of the Kurbernetes API.
	
- Ensuring and testing that the cluster has at least 3 nodes and 3 control plane nodes in place, will ensure that rolling updates can be performed to the back-end services without any down time.
The tester could make use of the Kurbernetes API in order to check this.

## 2. Ensuring the cluster is self healing and each node contains replicas of each pod:

- I would want to make sure the deployment configuration within the control plane is setup to continuously monitor the node instances, so that if an application node hosting the back-end were to go down, the deployment
controller automatically replaces the instance on another node in the cluster.

- Studying the deployment config should indicate whether there are multiple pods and whether the pods themselves are actually replicas or not.

This could be managed and checked by the tester by using the Kubectl CLI:

Some kubectl commands which could be used:
 
- kubectl get - list resources
- kubectl describe - show detailed information about a resource
- kubectl logs - print the logs from a container in a pod
- kubectl exec - execute a command on a container in a pod

## 3. Other than these checks and balances, I'd make sure the todo list API is working as expected via Postman by running the standarded test cases via the API.
