# 4.2 End-to-End Scenarios

Run the complete LC transaction lifecycle against the deployed blockchain network.

---

## Scenario 1 — Happy Path LC

Simulate the full lifecycle from application to payment release.

```bash
npm run e2e -- --scenario happy-path-lc
```

The test runner will:

| Step | Action | Expected Status |
|------|--------|----------------|
| 1 | Apply for LC | `APPLIED` |
| 2 | Issue LC | `ISSUED` |
| 3 | Advise LC | `ADVISED` |
| 4 | Present documents | `DOCUMENTS_PRESENTED` |
| 5 | Approve documents | `DOCUMENTS_APPROVED` |
| 6 | Release payment | `SETTLED` |

---

## Scenario 2 — Document Discrepancy

Test the rejection and re-submission flow.

```bash
npm run e2e -- --scenario document-discrepancy
```

Expected flow:
1. Documents presented with a mismatched amount.
2. Issuing bank rejects with reason `AMOUNT_MISMATCH`.
3. Beneficiary corrects and re-submits.
4. Documents approved on second attempt.

---

## Scenario 3 — LC Expiry

```bash
npm run e2e -- --scenario lc-expiry
```

Verifies that documents presented after the expiry date are automatically rejected by the smart contract.

---

## Running All E2E Scenarios

```bash
npm run e2e
```

Expected summary:

```
  E2E Scenarios
    ✔ Happy Path LC (1423ms)
    ✔ Document Discrepancy (2047ms)
    ✔ LC Expiry (891ms)

  3 passing (4s)
```

---

## ✅ Checkpoint

- [ ] All three E2E scenarios pass
- [ ] No unexpected errors in server logs during the run
- [ ] Blockchain explorer shows all transactions recorded

---

*Next: [Lab 5 — Deploy to IBM Cloud →](../lab5/01-deploy.md)*
