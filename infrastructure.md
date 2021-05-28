---
description: Generic Infrastructure Requirments
---

# Tech Infrastructure

## **Recommended**

1\) **Database:** Postgresql: 100GB SSD, minimum 4 core 16GB machine with multi-zone failover to start off.   \(Production\)  +  read replica to manage read APIs

2\) **Kubernetes Cluster**

3\) **Worker Nodes**: 4x  8core 32GB machines to start with on an autoscaling group with Kubernetes optimized machine images.

4\) **Load balancers**

5\) **SMS Gateway**. \(optional\)

6\) **Email server**

7\) 1 **VPN server**

8\) 1 **jump host** to manage the Kubernetes control plane

9\) Newrelic or datadog **Monitoring**

10\) **Redis Cluster**

