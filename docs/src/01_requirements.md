# Requirements

This section outlines the key requirements that guide the architecture and development of the Customer Experience (CX) product. It defines what the product must achieve from both a business and technical perspective, including expected quality attributes and system behaviors. These requirements are derived from the architectural diagrams, system context and business objectives provided by the Customer Experience team.

## Business Goals  

| ID    | Goal Description                                                                                |
| ----- | ----------------------------------------------------------------------------------------------- |
| BG-01 | Provide a centralized, scalable, and resilient system for managing VIP lounge invitations.      |
| BG-02 | Facilitate seamless integration with external service providers (AENA).                         |
| BG-03 | Improve traceability and observability of customer context (CTX) in all transactions.           |
| BG-04 | Ensure secure persistence and backup of operational and customer data.                          |


## Quality Goals


| Priority | Quality attribute | Description                                                            | Example scenario                          |
| -------- | ----------------- | ---------------------------------------------------------------------- | ----------------------------------------- |
| High     | Scalability       | System must scale to support traffic spikes,                           | Massive afluence of FF at airport.        |
| High     | Availability      | High availability across multiple AZs with no single point of failure. | One AZ fails, system continues operating. |
| Medium   | Performance       | APIs should respond within 200 ms.                                     | Frontends shold get immediate responses.  |
| Low      | Observability     | Full traceability of CX events through Dynatrace/Jaeger.               | Audit operations via logs.                |

**Note**: items pending validation. 


## Detailed requirements

The requirements are in confluence page:

https://transform.atlassian.net/wiki/spaces/DSO/pages/4798185473/VIP+-+Iberia+Madrid+VIP+lounge+invitation+management+-+v.1

[Back](../README.md)
