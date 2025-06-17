# Solution Strategy

The system adopts a service-oriented architecture, structured around the business capability of managing VIP Lounge Invitations for eligible customers. It is composed of independently deployable components that align with specific responsibilities in the customer journey, from UI interaction to QR-based lounge access.

| Layer                                 | Description                                                                                                                                                                       |
| ------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **User Interaction Layer**            | The customer interacts through the web or mobile app (User Interface), which communicates with backend components via an API Gateway.                                             |
| **CX Backend  (Business Logic)**      | The core logic is handled in a Java-based container `Invitation Mgr`, which generates and manages VIP invitation QR codes and coordinates all back-end validation and enrichment. |
| **QR Engine**                         | A dedicated component responsible for secure QR code generation and storage (claim-check pattern).                                                                                |
| **CRM Cloud Integration**             | Once a QR is generated, an event is pushed to CRM for outbound communication with the customer (e.g., email with QR, push event on mobile app, etc...).                           |
| **Loyalty Integration**               | Loyalty status is verified through a REST API to determine access eligibility.                                                                                                    |
| **Airport Lounge Interfaces**         | Iberia / AENA systems at the lounge physically query the API for validating QR codes and granting access.                                                                         |
| **Historical Storage**                | Final master data is pushed to IBDP (Iberia Data Platform) for traceability and analytics.                                                                                        |
| **Domain Enrichment Engine**          | A secondary engine performs domain-specific data recovery and enrichment (e.g., from IAGL or Resiber).                                                                            |


| Goal             | Strategy                                                                                   |
| ---------------- | ------------------------------------------------------------------------------------------ |
| **Scalability**  | Stateless containers behind an API Gateway; each component scales independently.           |
| **Resilience**   | Claim-check pattern with persistent QR store; decoupled CRM events.                        |
| **Security**     | QR codes are stored, not sent inline; access is verified at scan-time.                     |
| **Traceability** | All activity is recorded in IBDP; audit-ready structure.                                   |
| **Modularity**   | Business logic, QR engine, and integrations are loosely coupled and deployable separately. |



## C4 L1
![C4L1 diagram](./diagrams/VIPLoungeInvitation-C4%20L1.png "C4L1 diagram")

---

## C4 L2
![C4L2 diagram](./diagrams/VIPLoungeInvitation-C4%20L2.png "C4L2 diagram")

---

## C4 L3
![C4L3 diagram](./diagrams/VIPLoungeInvitation-C4%20L3.png "C4L3 diagram")



[Back](../README.md)
