# Architecture Constrains

| ID    | Constraint                                   | Summary                                                                                    |
| ----- | -------------------------------------------- | ------------------------------------------------------------------------------------------ |
| AC-01 | **AWS-Only Deployment**                      | All infrastructure and services must be hosted within AWS.                                 |
| AC-02 | **Multi-AZ Redundancy**                      | Services must be deployed across at least two availability zones.                          |
| AC-03 | **Use of ECS for Containers**                | All microservices must run on Amazon ECS, not EKS or other orchestrators.                  |
| AC-04 | **RDS Aurora for Persistent Storage**        | Main CX data must be stored in Amazon Aurora with RDS Proxy for access.                    |
| AC-05 | **EventBridge for Asynchronous Events**      | Inter-system asynchronous communication must use AWS EventBridge.                          |
| AC-06 | **No Direct DB Access from Frontend**        | All database access must go through API services, not directly from the frontend.          |
| AC-07 | **Use of API Gateway + ALB/NLB**             | All external access must be routed through AWS API Gateway and load balancers.             |
| AC-08 | **Cache with Local Redis**                   | CTX data must be cached locally using Redis for performance.                               |
| AC-09 | **Decoupled from Ancillaries**               | Customer Experience services must operate independently from Iberia.com ancillary systems. |
| AC-10 | **Compliance with Iberia Security Policies** | All components must adhere to Iberia’s security, data retention, and audit requirements.   |


[Back](../README.md)
