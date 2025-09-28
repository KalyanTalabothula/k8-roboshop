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

Example from your YAML:  
```yaml
kind: Service
metadata:
  name: mongodb
