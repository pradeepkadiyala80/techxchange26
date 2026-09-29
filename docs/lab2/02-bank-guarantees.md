# 2.2 Bank Guarantees

A **Bank Guarantee** is a promise by a bank to cover a loss if a borrower defaults on a loan or obligation. Unlike an LC, payment under a bank guarantee is triggered by non-performance rather than document presentation.

---

## Types of Bank Guarantees Covered

| Type | Use Case |
|------|---------|
| **Bid Bond** | Ensures a bidder will honour their bid |
| **Performance Bond** | Ensures contractor completes work |
| **Advance Payment Guarantee** | Protects buyer's advance payment |
| **Financial Guarantee** | General credit-support instrument |

---

## Key Differences: LC vs Bank Guarantee

| Aspect | Letter of Credit | Bank Guarantee |
|--------|-----------------|----------------|
| Primary mechanism | Payment on document presentation | Compensation on non-performance |
| Trigger | Compliant documents | Default / non-performance claim |
| Parties | 4 (applicant, beneficiary, issuing, advising) | 3 (applicant, beneficiary, guarantor bank) |
| Usage | Trade payments | Bid, performance, financial assurance |

---

## Smart Contract Functions — Bank Guarantee

| Function | Description |
|----------|-------------|
| `issueBankGuarantee` | Bank issues guarantee to beneficiary |
| `claimBankGuarantee` | Beneficiary claims due to non-performance |
| `contestClaim` | Applicant contests the claim |
| `settleBankGuarantee` | Bank settles the claim after adjudication |
| `expireBankGuarantee` | Marks guarantee as expired if no claim raised |

---

## Hands-On: Issue a Bank Guarantee

```bash
curl -s -X POST http://localhost:3000/api/bg/issue \
  -H "Content-Type: application/json" \
  -d '{
    "applicant": "ACME Corp",
    "beneficiary": "City Infrastructure Dept",
    "type": "PERFORMANCE",
    "amount": 100000,
    "currency": "USD",
    "expiryDate": "2026-12-31",
    "underlyingContract": "CONTRACT-2026-007"
  }' | jq .
```

Expected response:

```json
{
  "bgId": "BG-2026-0001",
  "status": "ISSUED",
  "txId": "e5f6g7h8..."
}
```

---

## ✅ Checkpoint

- [ ] You can distinguish between LC and Bank Guarantee
- [ ] You understand when each instrument is used
- [ ] `issueBankGuarantee` API call returns `BG-2026-0001`

---

*Next: [2.3 Documentary Collections →](03-documentary-collections.md)*
