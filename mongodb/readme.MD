# 🔹 Why do we need Service in Kubernetes?

## 1. Problem without Service
- Suppose you create a Deployment → it creates Pods.  
- But Pods ki IP address ane di static ga undadu.  

Example:  
- Today Pod IP = `10.42.0.5`  
- If Pod restarts, new IP = `10.42.0.8`  

App ki connection cheyyali ante → Pod IP maripothunte, direct ga connect cheyyalem.  

👉 So, we cannot depend on Pod IP directly.  

---

## 2. Solution = Service
- **Service** = fixed, permanent IP and DNS name for a set of Pods.  
- Even if Pods restart / IPs change → Service will automatically route traffic to correct Pods.  
- Manaki inka mongodb, catalogue tho connect avutmdhi by using the Service resources. 

Example from your YAML:  
```yaml
kind: Service
metadata:
  name: mongodb

👉 So in cluster, apps can always connect using:

mongodb.roboshop.svc.cluster.local:27017


(no need to care about Pod IPs).

3. How Service works?

Service uses selectors (labels) to find which Pods to forward traffic to.

selector:
  component: mongodb
  project: roboshop
  tier: database


👉 Any Pod with these labels = Service will send traffic there.

Example: if tomorrow Pod IP changes → still traffic goes, because labels are same.

4. Service Types (simplified)

ClusterIP (default) → accessible only inside cluster. (Your MongoDB case ✅)

NodePort → makes it accessible from outside using <NodeIP>:<NodePort>.

LoadBalancer → integrates with cloud load balancer (AWS/GCP/Azure).

5. Your Case (MongoDB)

Deployment creates a Pod → MongoDB runs inside.

Service gives a stable IP + DNS name for MongoDB.

So other apps in roboshop project (like catalogue, user, cart, etc.) can always connect using:

mongodb:27017


instead of chasing Pod IPs.

✅ In short (very simple):

Deployment = creates Pods (apps run here).

Pod IPs = temporary.

Service = permanent IP/DNS to reach those Pods reliably.