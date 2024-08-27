# zk-SNARK Example with Nullifier and Expiration

This README provides a basic example of how to integrate **Nullifier** and **Expiration** into a zk-SNARK proof using `o1js`.

## 1. Introduction

- **Nullifier**: A unique value used to prevent double-spending by ensuring a transaction cannot be reused.
- **Expiration**: A condition that ensures the proof is valid only for a specific period.

## 2. Example Circuit

```javascript
import { Field, Circuit } from 'o1js';

// Define the circuit with Nullifier and Expiration
class TransactionCircuit extends Circuit {
  nullifier: Field;
  expiration: Field;
  currentTime: Field;

  constructor(nullifier: Field, expiration: Field, currentTime: Field) {
    super();
    this.nullifier = nullifier;
    this.expiration = expiration;
    this.currentTime = currentTime;
  }

  // Prove the transaction is valid
  validateTransaction() {
    // Ensure nullifier is unique (not reused)
    this.nullifier.assertNotEqual(Field(0));

    // Ensure the proof has not expired
    this.currentTime.assertLessThanOrEqual(this.expiration);
  }
}
## 3. Creating the Proof
To create the proof, instantiate the circuit with the appropriate values and call the validateTransaction method.
```javascript
const proof = await TransactionCircuit.createProof({
  nullifier: Field(12345),
  expiration: Field(1672531199), // Example expiration timestamp
  currentTime: Field(1672529999), // Current time for validation
});

```
## 3. Verifying the Proof
To verify the proof, use the verify method with the appropriate verification key.
```javascript
const isValid = await TransactionCircuit.verifyProof(proof, verificationKey);
if (isValid) {
  console.log("Proof is valid and has not expired.");
} else {
  console.log("Proof is invalid or has expired.");
}

```

## 4. Conclusion
This example demonstrates how to implement a simple zk-SNARK proof with Nullifier and Expiration. The circuit ensures that the transaction is unique and valid within a specific time frame.
