# Solution Strategy Initial Vision

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


# SOLUTION STRATEGY V2

## Summary
The Invitation Manager Initiative involves several services, each with its specific functionality, working together to provide a comprehensive invitation manager solution. Here is a summary of the services involved:

- User Interface - React interface:
    - Responsible for the user interface.
    - Check to create only invitations allowed by the boarding pass or Iberia Card Type.
    - CRUD user interface for the invitations.
    

- Invitations Manager - Invitation Manager Microservice:
    - Retrieves information about allowed invitations.
    - Expose the API REST functions for CRUD operations.
    - Create new invitations
    - Generate QR code and save to S3 bucket (for Iberia)
    - Call AENA API Interface to create QR (for FastTrack and AENA Lounges)
    - Communicate with CRM Cloud or MKT Cloud to send email.
    - Validate QR (only Iberia)
    - Reedem QR (only Inberia)


- Card Type Manager - Manage information about card type:
    - Ask IAGL about card type information of a member and relates it to number of invitations
    - Retrieves information about card type allowed invitations information.
    

- AENA API - Interface with AENA to buy products
    - API to buy invitations to fastTrack and AENA VIP Lounges
    - Generate a QR Code to access
    - Communicate with AENA internal systems to allow the invitation
 
- MKT Cloud - Interface with AENA to buy products
    - API to buy invitations to fastTrack and AENA VIP Lounges

- ASSECO - Readers in Iberia VIP Lounges:
    - Read QR Code
    - Send information to Invitations Manager to validate the code
    - Validate the name of the inviter against boarding card name
    - Communicate open the door

- SalesForces
    - Receive a request from ASSECO for the invitation
    - Check if the VIP is the lounge
    - Call to Invitations Manager to Redeem the QR
    - Show in salesforces a popup to the operator to open the door
    - ¿How is going to be the flow when we have automatic doors?

- AENA FastTrack/Automatic doors
    - Check if the QR generated by AENA is valid
    - ¿Check the name of the invitated?
    - Open the door or show a message if don't

- IAGL 
    - External system that retrieves information about loyalty system
    - Used to get the card type associated to the member
    - In a future it would be desirable this system retrieves information related to invitations associated to the member (strategic solution)

- CRM Cloud (Only in strategic solution)
    - System in development at this moment, that it will be the interface with CRM
    - In the strategic solution, the call to send the email should be managed by this service
    - In the strategic solution, the call received from SalesForce to redeem QR should be managed by this service

    


# MVP Solution

In the MVP Solution we have 2 considerations:
- CRM Cloud is delayed, then we will connect directly to MKT Cloud with the compromise to change to CRM Cloud when it is going to be ready.
- CardType Manager Loyalty microserice is going to be deployed in Cx accounts, but the final repository is in Loyalty accounts.

## C4 L2 Initial
![C4L2 MVP](./diagrams/Invitation-C4-L2-Initial.svg "C4L2 MVP")


# Strategic Solution
## C4 L2 Strategic
![C4L2](./diagrams/Invitation-C4-L2-Strategic.svg "C4L2")


[Back](../README.md)
