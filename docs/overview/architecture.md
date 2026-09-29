# Architecture Overview

This section describes the high-level architecture of the Trade Finance solution you will build during the labs.

---

## Component Diagram

```
┌─────────────────────────────────────────────────────────────┐
│                        IBM Cloud                            │
│                                                             │
│  ┌──────────────┐    ┌──────────────┐   ┌───────────────┐  │
│  │  API Gateway │───▶│  Node.js App │──▶│  IBM Blockchain│  │
│  │  (API Connect│    │  (Express)   │   │  Platform     │  │
│  └──────────────┘    └──────────────┘   └───────────────┘  │
│          │                  │                   │           │
│          │           ┌──────┴──────┐            │           │
│          │           │  Cloudant   │            │           │
│          │           │  (Documents)│            │           │
│          │           └─────────────┘            │           │
└──────────┼──────────────────────────────────────┼───────────┘
           │                                      │
     ┌─────▼─────┐                        ┌───────▼──────┐
     │  Importers │                        │  Exporters   │
     │  (Buyers)  │                        │  (Sellers)   │
     └────────────┘                        └──────────────┘
```

---

## Key Components

### 1. API Gateway (IBM API Connect)
Handles authentication, rate-limiting, and routing of all inbound trade finance requests.

### 2. Application Server (Node.js / Express)
Implements the business logic for:
- LC issuance and amendment
- Document submission and verification
- Payment release triggers

### 3. IBM Blockchain Platform
Runs the **Hyperledger Fabric** smart contracts (chaincode) that enforce trade rules and provide an immutable audit trail.

### 4. Cloudant (Document Store)
Stores trade documents (invoices, bills of lading, certificates of origin) as JSON documents with attachment support.

---

## Data Flow

1. **Importer** submits an LC application via the API Gateway.
2. The **Application Server** validates the request and invokes the smart contract.
3. The **smart contract** records the LC on the blockchain and emits an event.
4. The **Exporter** receives notification and submits shipping documents.
5. Documents are stored in **Cloudant** and their hashes are anchored on-chain.
6. Upon document approval, the smart contract triggers payment release.

---

*Next: [Lab 1 — Accessing IBM Cloud →](../lab1/01-ibm-cloud-access.md)*
