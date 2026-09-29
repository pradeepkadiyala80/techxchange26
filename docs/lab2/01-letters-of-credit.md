# 2.1 Letters of Credit (LC)

A **Letter of Credit** is a guarantee from a bank that a buyer's payment to a seller will be received on time and for the correct amount. In this section you will explore the LC lifecycle and how it maps to smart contract functions.

---

## Key Concepts

| Term | Definition |
|------|-----------|
| **Applicant** | The buyer / importer who requests the LC |
| **Beneficiary** | The seller / exporter who receives payment |
| **Issuing Bank** | The buyer's bank that issues the LC |
| **Advising Bank** | The seller's bank that advises the LC |
| **Tenor** | The time period within which documents must be presented |

---

## LC Lifecycle

```
Applicant ──apply──▶ Issuing Bank ──issue──▶ Advising Bank ──advise──▶ Beneficiary
                                                                              │
                                                              ship goods       │
                                                              & submit docs    ▼
Applicant ◀──pay── Issuing Bank ◀──claim── Advising Bank ◀──present── Beneficiary
```

---

## Smart Contract Functions — LC

The `LC` chaincode exposes these functions:

| Function | Caller | Description |
|----------|--------|-------------|
| `applyLC` | Applicant | Submits a new LC application |
| `issueLC` | Issuing Bank | Issues the LC after credit approval |
| `adviseLC` | Advising Bank | Confirms receipt to beneficiary |
| `presentDocuments` | Beneficiary | Submits shipping documents |
| `approveDocuments` | Issuing Bank | Approves documents and releases payment |
| `rejectDocuments` | Issuing Bank | Rejects with a discrepancy reason |
| `closeLC` | System | Marks the LC as closed after settlement |

---

## Hands-On: Apply for an LC

Using the REST API (which you will build in Lab 3), apply for an LC:

```bash
curl -s -X POST http://localhost:3000/api/lc/apply \
  -H "Content-Type: application/json" \
  -d '{
    "applicant": "ACME Corp",
    "beneficiary": "GlobalShip Ltd",
    "amount": 50000,
    "currency": "USD",
    "expiryDate": "2026-06-30",
    "goods": "Industrial Machinery — 10 units"
  }' | jq .
```

Expected response:

```json
{
  "lcId": "LC-2026-0001",
  "status": "APPLIED",
  "txId": "a1b2c3d4..."
}
```

---

## ✅ Checkpoint

- [ ] You understand the roles in an LC transaction
- [ ] You can describe the LC lifecycle in your own words
- [ ] The `applyLC` API call returns `LC-2026-0001`

---

*Next: [2.2 Bank Guarantees →](02-bank-guarantees.md)*
