# K8s Exam Q and A

##
**Q.1**
You have been asked to create a new ClusterRole for a deployment pipeline and bind it to a specific ServiceAccount scoped to a specific namespace.

**Task** 

[Question and Answe URL](https://www.itexams.com/exam/CKA)

Create a new ClusterRole named deployment-clusterrole, which only allows to create the following resource types:

**Deployment,**
**Stateful Set,**
**DaemonSet**

Create a new ServiceAccount named __cicd-token__ in the existing namespace __app-team1.__
Bind the new ClusterRole __eployment-clusterrole__ to the new ServiceAccount __cicd-token__, limited to the namespace __app-team1__


**Step-1: Create ClusterRole**

```bash
kubectl create clusterrole deployment-clusterrole --verb=create --resource=deployments,statefulsets,daemonsets --api-group=apps
```

**Step-2: Create RoleBinding:**

```bash
kubectl create serviceaccount cicd-token -n app-team1
```
**Step-3: Create ServiceAccount:**

```bash
kubectl create rolebinding cicd-rolebinding \
  --clusterrole=deployment-clusterrole \
  --serviceaccount=app-team1:cicd-token \
  -n app-team1
```

### Configuration Verification

****Verify the ClusterRole, ServiceAccount, RoleBinding****
```bash
kubectl describe clusterrole deployment-clusterrole

kubectl get serviceaccount cicd-token -n app-team1

kubectl describe rolebinding cicd-rolebinding -n app-team1
```


##
**Q.2**
Set the node named ek8s-node-0 as unavailable and reschedule all the pods running on it.

**Task** 

[Question and Answe URL](https://www.itexams.com/exam/CKA)


**Step-1: Cordon the Node (mark as unschedulable) :**

```bash
kubectl cordon ek8s-node-0
```

**Step-2: Drain the Node (evict pods and reschedule) :**

```bash
kubectl drain ek8s-node-0 --ignore-daemonsets --delete-local-data
```


### Configuration Verification

****Verify Node and Pod Status:****

```bash
kubectl get nodes

kubectl get pods --all-namespaces -o wide
```
