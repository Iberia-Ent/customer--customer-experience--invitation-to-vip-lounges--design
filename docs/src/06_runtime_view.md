# Runtime View

It describes concrete behavior and interactions of the system’s building blocks in form of scenarios from the following areas:

- Sequence Diagrams use to deine the main Use Cases and interactions.
- Operation and administration: launch, start-up, stop
- Error and exception scenarios

## VIP Reservation Iberia Lounge
![Sequence diagram](./diagrams/IberiaSequenceDiagram.svg "Sequence diagram")

1.- The system checks the available invitations in the Invitation Manager.
2.- It calls the Loyalty system to check the number of invitations assigned to the  member's Iberia Card type.
3.- The system check the invitations already assigned in the database. If invitations are available, it allows to create invitation
4.- In the User interface the VIP fills the data in the guest's details (name, surname, and flight number).
5.- The system validates the information and save the invitation in the database
6.- It calls the CRM to generate and send an email.




## AENA Reservation Iberia Lounge
![Sequence diagram](./diagrams/AENASequenceDiagram.svg "Sequence diagram")
1.- The system checks the available invitations in the Invitation Manager.
2.- It calls the Loyalty system to check the number of invitations assigned to the  member's Iberia Card type.
3.- The system check the invitations already assigned in the database. If invitations are available, it allows to create invitation
4, 5 and 6: The system calls to AENA interfaces to check the availability of the lounges or fasttrack.
7.- In the User interface the VIP fills the guest's details (name, surname and flight number)
8.- The system validates the information and create the invitation
9.- Reserve the lounge or fasttrack service in AENA.
9.- Save the invitation in the database.
10.-The system calls to CRM to generate and send an email.


## Guest entrance to Iberia Lounge
![Sequence diagram](./diagrams/IberiaEntranceSequenceDiagram.svg "Sequence diagram")
1.- The guest presents the QR code.
2.- The system calls the Invitations Manager to validate the QR.
3.- The guest presents their  boarding pass
4.- ASSECO system validates the passenger's name 
5.- The system calls to SalesForces to check if the VIP is already in the lounge.
6.- If all validations are successful, the QR is redeemed.

## Guest entrance to AENA Lounge
The validations are performed by AENA, no Iberia flow involved.

[Back](../README.md)
