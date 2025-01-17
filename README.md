### Comprehensive Working Document: Enshrined Functionality Framework for a Custom Layer 1 Protocol

#### **1. Vision and Goals**

The objective of this custom enshrined functionality framework is to embed native Layer 2 (L2) support into a Layer 1 (L1) blockchain protocol, enabling scalability, security, and interoperability. By designing the framework with modularity and flexibility, we aim to standardize rollup operations, optimize performance, and reduce costs for developers and users.

##### **Real-World Applications**

1. **Decentralized Finance (DeFi)**: Enable high-throughput, low-cost transactions for platforms like decentralized exchanges, lending protocols, and automated market makers.
2. **Gaming and NFTs**: Support seamless, low-latency interactions in blockchain-based gaming, including in-game assets and non-fungible token (NFT) marketplaces.
3. **Cross-Border Payments**: Facilitate scalable, trustless, and affordable international payment systems with fast settlement times.
4. **Supply Chain Management**: Provide transparency and efficiency for tracking goods, ensuring real-time updates and cost-efficient operations across global supply chains.
5. **Identity and Credential Verification**: Create interoperable, secure systems for managing digital identities and credentials without exposing private information.

##### **Key Goals**

1. **Native Scalability**: Optimize data availability, transaction processing, and proof verification.
2. **Enhanced Security**: Ensure rollups inherit robust security guarantees from the L1.
3. **Interoperability**: Facilitate seamless communication between L1 and L2, and across multiple L2s.
4. **Cost Efficiency**: Minimize operational expenses, especially for data storage and execution.
5. **Developer Accessibility**: Provide standardized APIs, tooling, and resources for simplified development.

---

#### **2. Framework Components**

##### **A. Data Availability Layer**

**Purpose**: Offer scalable, efficient, and cost-effective data storage for rollups while ensuring availability for verification.

**Features**:

1. **Data Blobs**:
   - Introduce a new transaction type optimized for rollup data, with reduced costs compared to traditional calldata.
   - Temporary storage for a defined period (e.g., 1,000 blocks) to minimize L1 overhead.
2. **Sampling-Based Availability**:
   - Implement Danksharding principles to enable validators to sample data rather than store it fully.
   - Use cryptographic proofs to verify data availability and integrity.
3. **Incentivized Storage**:
   - Reward validators for participating in data availability sampling through periodic staking rewards or transaction fees tied to data blobs.
   - Validators compete to be part of the sampling process, ensuring decentralized participation and incentivizing timely performance.

**Risks and Challenges**:

1. **Collusion Among Validators**:
   - Validators might collude to falsely report data availability. To mitigate this, cryptographic proofs and regular audits can ensure integrity.
2. **Performance Overhead**:
   - Sampling and cryptographic verification can introduce computational overhead. Optimization in proof generation and validation algorithms is necessary.
3. **Economic Attacks**:
   - Validators could manipulate fees or incentives. Dynamic incentive structures that adjust based on validator performance can address this.
4. **Data Unavailability**:
   - Temporary network failures or validator dropout can lead to data unavailability. Redundancy mechanisms and fallback protocols ensure continuity.

##### **B. Proof Verification System**

**Purpose**: Provide L1-native support for verifying rollup state transitions securely and efficiently.

**Features**:

1. **Integrated Proof Verifiers**:
   - Embed zk-SNARK and zk-STARK verifiers directly into the protocol.
   - zk-SNARKs are optimized for minimal proof sizes and faster verification, making them suitable for applications requiring frequent state updates, such as decentralized exchanges or gaming platforms.
   - zk-STARKs, which eliminate the need for trusted setups, are ideal for large-scale computations like batch verifications in machine learning or supply chain tracking.
   - Example Workflow:
     - A zk-SNARK-enabled rollup submits a validity proof for processed transactions.
     - Validators use the zk-SNARK verifier to confirm correctness, enabling near-instantaneous state transitions.
     - Alternatively, zk-STARK proofs for a batch of transactions are verified in parallel, ensuring scalability for high-throughput rollups.
2. **Universal Proof Interface**:
   - Standardized API for submitting and verifying proofs, compatible with various rollup designs.
   - Example API Call:

     ```json
     {
       "rollup_id": "rollup_123",
       "proof_type": "zk_snark",
       "proof_data": "base64_encoded_proof"
     }
     ```

   - Validators receive the proof, perform verification, and update the global state tree.
3. **Batch Verification**:
   - Enable efficient batch verification for zk proofs, reducing computational costs.
   - Example Use Case:
     - A zk-STARK-enabled rollup processes 10,000 transactions in a batch and generates a single proof.
     - Validators perform a one-time verification for the entire batch, drastically reducing per-transaction overhead.

##### **C. Decentralized Sequencer Framework**

**Purpose**: Ensure fairness and prevent centralization in transaction sequencing.

**Features**:

1. **Shared Sequencer Pools**:
   - Validators act as decentralized sequencers, rotating or competing based on predetermined criteria.
2. **Priority Fees**:
   - Incentivize sequencers with priority fees for faster transaction ordering.
3. **Fair Sequencing Mechanisms**:
   - Incorporate cryptographic randomness or consensus-based ordering to ensure fairness.

##### **D. Cross-Rollup Composability**

**Purpose**: Enable seamless, trustless interactions between rollups and the L1.

**Features**:

1. **Synchronous Messaging**:
   - Support atomic cross-rollup contract calls and data sharing.
   - **Example Use Case**:
     - A user on Rollup A wants to purchase an NFT listed on Rollup B. The transaction involves two steps:
       1. The user initiates the purchase request on Rollup A, which generates a message containing the user's intent and payment details.
       2. This message is synchronized with Rollup B via L1, triggering the contract on Rollup B to validate the payment and complete the NFT transfer back to Rollup A.
       - Validators ensure the state updates are atomic, preventing partial execution or errors.
2. **Shared State Trees**:
   - Maintain a global state tree on L1 to track and manage rollup states.
   - **Workflow Example**:
     - Rollup A and Rollup B publish state updates to the shared state tree.
     - When a cross-rollup interaction occurs, the shared state tree verifies the integrity of both states and synchronizes the transaction.
3. **Bridgeless Transfers**:
   - Facilitate direct asset and state transfers between rollups, eliminating dependency on bridges.
   - **Example Workflow**:
     - A user transfers tokens from Rollup A to Rollup B using a bridgeless mechanism:
       1. The tokens are locked on Rollup A.
       2. A proof of the locked state is submitted to L1.
       3. Rollup B acknowledges the proof and mints an equivalent amount of tokens for the user.

##### **E. Cost Optimization Mechanisms**

**Purpose**: Reduce operational costs for rollups and enhance user affordability.

**Features**:

1. **Calldata Compression**:
   - Implement cryptographic compression techniques to minimize the size of rollup data posted to L1.
2. **Dynamic Gas Pricing**:
   - Adjust gas fees dynamically based on network load and demand, optimizing cost-efficiency.

##### **F. Governance and Upgradability**

**Purpose**: Allow iterative improvements to the framework without compromising decentralization or security.

**Features**:

1. **Rollup Governance Modules**:
   - Provide a mechanism for rollups to propose and vote on upgrades or new features.
2. **Decentralized Voting**:
   - Enable L1 stakeholders to participate in decisions regarding enshrined functionality updates.

---

#### **3. Workflow: Layer 2 Interaction with Enshrined Functionality**

##### **A. Data Posting**

1. Rollup batches transactions and generates a cryptographic proof.
2. The batch data is compressed into a blob and submitted to L1.
3. Validators ensure data availability using sampling techniques, rewarding honest participation.

##### **B. Proof Verification**

1. Rollup submits either a validity proof or fraud proof to L1.
2. The integrated proof verification system validates the submission.
3. Successful validation finalizes the rollup state transition on L1.

##### **C. Sequencing**

1. Rollup transactions are submitted to a shared sequencer pool.
2. Validators sequence transactions fairly, prioritizing those with higher fees.
3. Ordered transactions are posted back to L1 for settlement and execution.

##### **D. Cross-Rollup Interaction**

1. A user initiates an asset transfer or interaction between Rollup A and Rollup B.
2. The transfer is routed through L1 using synchronous messaging and the shared state tree.
3. Rollup B processes the interaction without requiring a bridge.

---

#### **4. Implementation Considerations**

##### **A. Consensus Mechanism**

- Use Proof-of-Stake (PoS) for scalability, energy efficiency, and robust security.
- Validators handle tasks such as proof verification, data availability sampling, and sequencing.

##### **B. Security Assumptions**

- Ensure Byzantine fault tolerance to maintain trustless operations.
- Provide incentives to validators for honest participation in data and proof handling.

##### **C. Rollup Agnosticism**

- Design the framework to support both Optimistic and zk-Rollups.
- Standardized interfaces ensure compatibility across diverse rollup implementations.

---

#### **5. Technical Examples**

This section demonstrates detailed workflows and specific examples of how APIs interact with validators and rollups in real-time to provide seamless functionality.

##### **A. Rollup Data Blob Storage**

Define a new transaction type for storing rollup data:

```json
{
  "type": "data_blob",
  "rollup_id": "rollup_123",
  "data": "base64_encoded_blob",
  "expiry": "block_+_1000"
}
```

**Workflow Example**:

1. **Step 1**: A rollup submits a batch of transactions to the L1 in the form of a compressed data blob.
2. **Step 2**: Validators sample the data for availability, ensuring it meets protocol standards.
3. **Step 3**: If the data passes sampling, it is temporarily stored in L1 for the specified expiry period.
4. **Step 4**: Rewards are distributed to validators for their sampling efforts, incentivizing participation.

##### **B. Proof Submission Endpoint**

Provide an API endpoint for proof submissions:

```
POST /api/rollup/proof
{
  "rollup_id": "rollup_123",
  "proof_type": "zk_snark",
  "proof_data": "proof_payload"
}
```

**Workflow Example**:

1. **Step 1**: The rollup generates a zk-SNARK validity proof after processing transactions.
2. **Step 2**: The proof is submitted to the L1 via the `/api/rollup/proof` endpoint.
3. **Step 3**: Validators verify the proof using integrated zk-SNARK verifiers.
4. **Step 4**: Upon successful verification, the rollup’s state transition is finalized, ensuring trustless execution.

##### **C. Shared Sequencer Registration**

Smart contract to register sequencers:

```solidity
contract SequencerRegistry {
    mapping(address => bool) public isSequencer;
    function register() external { ... }
}
```

**Workflow Example**:

1. **Step 1**: A validator sends a transaction to the `SequencerRegistry` contract, registering as a sequencer.
2. **Step 2**: The contract updates its mapping, marking the validator as an active sequencer.
3. **Step 3**: Registered sequencers participate in transaction ordering for rollups, ensuring decentralization and fairness.
4. **Step 4**: Sequencers are rewarded with priority fees for processing transactions efficiently.

These examples illustrate the practical application of enshrined functionality, emphasizing the interactions between rollups, validators, and the L1 protocol.

---

#### **6. Benefits**

1. **Scalability**: Reduces transaction fees and enhances throughput.
2. **Security**: Ensures rollups inherit the strong security guarantees of L1.
3. **Interoperability**: Facilitates seamless interactions across rollups and L1.
4. **Cost Efficiency**: Optimized data handling minimizes user costs.
5. **Developer Accessibility**: Modular and standardized components simplify development.

---



This custom enshrined functionality framework establishes a robust foundation for scaling Layer 1 protocols while supporting a diverse and innovative Layer 2 ecosystem.
