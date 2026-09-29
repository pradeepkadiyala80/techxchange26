# 4.1 Unit Testing

Write and run unit tests for the LC smart contract using the **Fabric Contract API** test framework.

---

## Test Framework

The project uses **Mocha** + **Chai** + **sinon** for unit testing chaincode:

```bash
npm test
```

---

## Writing a Test

```javascript
// test/lc-contract.test.js
const { Context } = require('fabric-contract-api');
const { ChaincodeStub } = require('fabric-shim');
const sinon = require('sinon');
const chai  = require('chai');
const { expect } = chai;

const LCContract = require('../chaincode/lc/lc-contract');

describe('LCContract', () => {
    let contract, ctx, stub;

    beforeEach(() => {
        contract = new LCContract();
        ctx      = sinon.createStubInstance(Context);
        stub     = sinon.createStubInstance(ChaincodeStub);
        ctx.stub  = stub;
        stub.getTxID.returns('txid-unit-test-001');
    });

    describe('applyLC', () => {
        it('should create a new LC with APPLIED status', async () => {
            const result = await contract.applyLC(
                ctx,
                'ACME Corp',
                'GlobalShip Ltd',
                '50000',
                'USD',
                '2026-06-30',
                'Industrial Machinery'
            );
            expect(result.status).to.equal('APPLIED');
            expect(result.amount).to.equal(50000);
            sinon.assert.calledOnce(stub.putState);
            sinon.assert.calledOnce(stub.setEvent);
        });
    });
});
```

---

## Running the Tests

```bash
npm test
```

Expected output:

```
  LCContract
    applyLC
      ✔ should create a new LC with APPLIED status (12ms)

  1 passing (45ms)
```

---

## Code Coverage

```bash
npm run test:coverage
```

The coverage report is generated at `coverage/index.html`. Open it in your browser:

```bash
open coverage/index.html    # macOS
xdg-open coverage/index.html  # Linux
```

Target: **≥ 80% line coverage** for all chaincode files.

---

## ✅ Checkpoint

- [ ] All unit tests pass (`npm test`)
- [ ] Code coverage report generated
- [ ] Line coverage ≥ 80%

---

*Next: [4.2 End-to-End Scenarios →](02-e2e-scenarios.md)*
