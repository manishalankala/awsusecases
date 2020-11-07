
# EKS AWS Cluster Architecture


```
VPC with 6 Subnets.
1.1 two Public Subnets (for web tier)
1.2 two Application Subnets (for middleware tier)
1.3 two Database Subnets (backend tier)


# To establish the communication between web layer pods to the middleware pods
A service should be created with type ClusterIP. 

# To establish the communication between middleware pods to the backend RDS database
A service should be created with type ExternalIP

# To expose the application to the end customers
Weblayer pods should be exposed as a NodePort service.


# Readiness Probe: Sometimes, pods are temporarily unable to serve traffic. For example pods need to load large data or configuration files during startup, or depend on external services like RDS after startup. In such cases we shouldn't kill the Pod, but we don't want to send it requests either. Kubernetes provied Readiness probes to detect and mitiagate these situations.
  
# Liveness Probe: Many pods running for long periods of time eventually transition to broken status, and cannot recover except by being restarted. Using Liveness probes we can detect and remedy such situations.

```


![image](https://user-images.githubusercontent.com/33985509/98441250-6ea42d00-20fd-11eb-8798-a45a60785b49.png)


![image](https://user-images.githubusercontent.com/33985509/98441330-df4b4980-20fd-11eb-9437-1f707b989bf9.png)
