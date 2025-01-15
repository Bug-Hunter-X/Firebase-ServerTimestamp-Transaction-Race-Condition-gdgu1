# Firebase ServerTimestamp Transaction Race Condition

This repository demonstrates a subtle bug involving Firebase's `FieldValue.serverTimestamp()` within transactions. Under high concurrency, the transaction intermittently fails with an unusual error message (`Error: Write on snapshot with pending write`), making debugging challenging. The root cause is a race condition between concurrent updates using server timestamps.

## Bug Description
Multiple clients updating the same document's field concurrently using `FieldValue.serverTimestamp()` within transactions can lead to inconsistent state and transaction failures.  The error message provided by Firebase is not standard, making diagnosis difficult.

## Solution
The solution involves optimizing the transaction logic to handle potential race conditions and adding appropriate error handling and retry mechanisms.  This often requires more sophisticated synchronization techniques to prevent conflicting write attempts.

## Setup
1.  Install Firebase:
   ```bash
   npm install firebase
   ```
2.  Configure Firebase (replace with your project credentials):
   ```javascript
   import { initializeApp } from "firebase/app";
   import { getFirestore, FieldValue, runTransaction } from "firebase/firestore";
   // ... Your Firebase config
   ```

## Reproduction Steps
1. Run the `bug.js` to reproduce the race condition and intermittent transaction failures.
2.  Observe the error messages in the console.
3. Run the `bugSolution.js` to see how the issue can be addressed.
