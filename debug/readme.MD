# 🐳 Debug Dockerfile – Explanation

## 🔎 What’s Happening Here?

- **Base Image** → `almalinux:9` (lightweight Linux distro).  
- **Install tools** → `telnet`, `net-tools`, `iputils`  
  - Useful for testing network connectivity.  
  - Commands like `ping`, `ifconfig`, `netstat`, `telnet` become available.  
- **Create user** → `roboshop` (so you don’t run as root).  
- **Switch user** → container runs as `roboshop`.  
- **CMD sleep** → keeps container running for a long time (like a playground pod for testing).  

---

## 🎯 Purpose of This Debug Image

This is a **debugging helper container** (not for production).  

👉 Mainly used for **network troubleshooting** inside **Kubernetes or Docker**.

You can use it to:

- ✅ Test `ping` between Pods/Services  
- ✅ Test **DNS resolution** (`ping google.com`, `ping mongodb.roboshop.svc.cluster.local`)  
- ✅ Test ports with `telnet <service> <port>`  
- ✅ Use `curl` (if installed — not included here, but can be added)  
- ✅ Run `ifconfig`, `netstat` to inspect container’s network  

---

## 🚀 Simple Answer

This **debug Dockerfile** is needed to **check networking between services** in Kubernetes/Docker (`ping`, `telnet`, DNS lookup).  
It is **not only for curl** — it’s for **general network debugging**.  
