# 2.3 Documentary Collections

A **Documentary Collection** is a trade finance mechanism where the exporter's bank (remitting bank) sends documents to the importer's bank (collecting bank), which releases them only upon payment or acceptance of a draft.

---

## Types

| Type | Abbreviation | Documents Released When |
|------|-------------|------------------------|
| Documents against Payment | D/P | Importer pays immediately |
| Documents against Acceptance | D/A | Importer accepts a time draft |

---

## Process Flow

```
Exporter ──docs──▶ Remitting Bank ──collection order──▶ Collecting Bank
                                                               │
                                                    present to importer
                                                               │
                                                               ▼
Exporter ◀──remit── Remitting Bank ◀──payment/acceptance── Importer
```

---

## Smart Contract Functions — Documentary Collection

| Function | Description |
|----------|-------------|
| `initiateCollection` | Exporter initiates collection with document hash |
| `presentToImporter` | Collecting bank presents documents |
| `payOrAccept` | Importer pays (D/P) or accepts draft (D/A) |
| `remitProceeds` | Collecting bank remits funds to remitting bank |
| `closeCollection` | Final settlement recorded on-chain |

---

## Hands-On: Initiate a Collection

```bash
curl -s -X POST http://localhost:3000/api/dc/initiate \
  -H "Content-Type: application/json" \
  -d '{
    "exporter": "GlobalShip Ltd",
    "importer": "ACME Corp",
    "type": "DP",
    "amount": 25000,
    "currency": "USD",
    "documentHash": "sha256:abc123...",
    "draftTenor": "AT SIGHT"
  }' | jq .
```

Expected response:

```json
{
  "dcId": "DC-2026-0001",
  "status": "INITIATED",
  "txId": "i9j0k1l2..."
}
```

---

## ✅ Checkpoint

- [ ] You understand the D/P vs D/A distinction
- [ ] You can trace the documentary collection flow
- [ ] `initiateCollection` API call returns `DC-2026-0001`

---

*Next: [Lab 3 — Smart Contracts →](../lab3/01-smart-contracts.md)*
