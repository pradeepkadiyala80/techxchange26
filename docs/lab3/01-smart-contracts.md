# 3.1 Smart Contracts

In this section you will write and deploy the Letter of Credit smart contract (chaincode) on IBM Blockchain Platform.

---

## Project Structure

```
chaincode/
├── lc/
│   ├── index.js          ← entry point
│   ├── lc-contract.js    ← LC chaincode logic
│   └── package.json
├── bg/
│   ├── index.js
│   ├── bg-contract.js
│   └── package.json
└── dc/
    ├── index.js
    ├── dc-contract.js
    └── package.json
```

---

## Step 1 — Review the LC Contract

Open [`chaincode/lc/lc-contract.js`](../../chaincode/lc/lc-contract.js) and examine the `applyLC` transaction:

```javascript
async applyLC(ctx, applicant, beneficiary, amount, currency, expiryDate, goods) {
    const lcId = `LC-${new Date().getFullYear()}-${ctx.stub.getTxID().slice(0, 6)}`;
    const lc = {
        lcId,
        applicant,
        beneficiary,
        amount: parseFloat(amount),
        currency,
        expiryDate,
        goods,
        status: 'APPLIED',
        createdAt: new Date().toISOString()
    };
    await ctx.stub.putState(lcId, Buffer.from(JSON.stringify(lc)));
    ctx.stub.setEvent('LC_APPLIED', Buffer.from(JSON.stringify({ lcId })));
    return lc;
}
```

Key points:
- State is stored using `putState` — it is persisted on the ledger.
- Events are emitted with `setEvent` — listeners can react in real time.
- The LC ID is derived from the transaction ID to ensure uniqueness.

---

## Step 2 — Package the Chaincode

```bash
cd chaincode/lc
npm install
cd ../..
ibmcloud blockchain chaincode package \
  --name lc-contract \
  --version 1.0.0 \
  --path chaincode/lc \
  --lang node \
  --output lc-contract.tar.gz
```

---

## Step 3 — Install on Peer

```bash
ibmcloud blockchain chaincode install \
  --peer peer0 \
  --package lc-contract.tar.gz
```

Note the **Package ID** from the output — you need it in the next step.

---

## Step 4 — Approve and Commit

```bash
# Replace PACKAGE_ID with the value from Step 3
ibmcloud blockchain chaincode approve \
  --channel trade-channel \
  --name lc-contract \
  --version 1.0.0 \
  --package-id PACKAGE_ID \
  --sequence 1

ibmcloud blockchain chaincode commit \
  --channel trade-channel \
  --name lc-contract \
  --version 1.0.0 \
  --sequence 1
```

---

## ✅ Checkpoint

- [ ] Chaincode packaged as `lc-contract.tar.gz`
- [ ] Chaincode installed and Package ID noted
- [ ] Chaincode approved and committed to `trade-channel`

---

*Next: [3.2 API Integration →](02-api-integration.md)*
