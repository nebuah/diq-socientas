Aquí tienes el siguiente capítulo.

---
## Capítulo 7: Infraestructura Técnica: Blockchain y Ethereum

Este capítulo provee depth técnico necesario para comprender cómo funciona la infraestructura que sustenta DI Q SOCIENTAS.

### 7.1 Fundamentos de Blockchain

**Definición:**

Blockchain es una estructura de datos distribuida, inmutable, y append-only que registra transacciones en bloques enlazados criptográficamente.

**Componentes:**

**1. Bloque:**

-   **Header:**
    -   `Previous Block Hash`: Cryptographic hash del bloque anterior (creates chain)
    -   `Timestamp`: Cuando bloque fue creado
    -   `Merkle Root`: Hash de todas transacciones en el bloque (permite verificación eficiente)
    -   `Nonce`: Número usado en Proof of Work para mining

-   **Body:**
    -   Lista de transacciones

**2. Chain:**

-   Secuencia de bloques enlazados via previous block hash
-   **Immutability:** Cambiar bloque anterior requiere rehacer todos bloques subsiguientes (computationally infeasible si chain es larga)

**3. Red Peer-to-Peer:**

-   **Nodes:** Computadoras corriendo client software
    -   **Full Nodes:** Store entire blockchain, validate todas transactions
    -   **Light Nodes:** Store solo headers, confían en full nodes para transaction data
-   **Network Propagation:** Nuevas transactions y bloques broadcast peer-to-peer

**4. Consensus:**

-   Mecanismo para acordar estado de blockchain entre nodes distribuidos
-   **Proof of Work (PoW):** Bitcoin, Ethereum pre-Merge
-   **Proof of Stake (PoS):** Ethereum post-Merge
-   (Detalles en 7.4)

**5. Cryptographic Primitives:**

**Hash Functions:**

-   **SHA-256 (Bitcoin):** Toma input de cualquier tamaño, produce 256-bit hash
-   **Keccak-256 (Ethereum):** Variante de SHA-3
-   **Properties:** Deterministic, quick to compute, infeasible to reverse, small input change → completely different hash

**Digital Signatures:**

-   **ECDSA (Elliptic Curve Digital Signature Algorithm):**
    -   Private key firma transacción
    -   Public key verifica signature
    -   Ensures: only holder de private key puede autorizar transacción
-   **Ethereum:** secp256k1 curve (same as Bitcoin)

**Public Key Cryptography:**

-   **Key Pair:** Private key (secret) + Public key (derivable from private)
-   **Address:** Derived from public key (Ethereum: last 20 bytes de Keccak-256 hash of public key)

**Merkle Trees:**

-   Binary tree where each leaf = hash de transaction, each node = hash de children
-   **Root (Merkle Root):** Single hash representing all transactions
-   **Benefit:** Efficiently prove transaction inclusion without revealing all transactions (SPV - Simplified Payment Verification)

**Immutability:**

Blockchain immutability resulta de:

1.  **Cryptographic Linking:** Cambiar bloque N invalida hash, rompe link con bloque N+1
2.  **Consensus:** Nodes reject invalid chains
3.  **Economic Cost:** Re-mining blocks (PoW) o re-staking (PoS) es prohibitively expensive

**Limitation:** Immutability is social consensus + economic cost, no absolute. Si mayoría de network agrees (hard fork), pueden revertir (ejemplo: Ethereum fork post-DAO hack).

---

### 7.2 Ethereum como Plataforma

**Historia:**

-   **2013:** Vitalik Buterin publica Ethereum whitepaper
-   **2014:** Crowdsale (~$18M raised)
-   **Julio 2015:** Mainnet launch (Frontier)
-   **2016:** The DAO hack, Ethereum/Ethereum Classic fork
-   **2017:** ICO boom
-   **2020:** DeFi Summer
-   **Septiembre 2022:** The Merge (PoW → PoS)

**Design Philosophy:**

Mientras Bitcoin es digital gold (store of value, simple payments), Ethereum es **world computer** —plataforma programmable para arbitrary logic.

**Account Model:**

Ethereum usa account model (vs. Bitcoin's UTXO):

**Two Account Types:**

1.  **Externally Owned Accounts (EOA):**
    -   Controlled by private key
    -   Can initiate transactions
    -   No code

2.  **Contract Accounts:**
    -   Controlled by code
    -   Cannot initiate transactions (solo respond to calls)
    -   Stores code (smart contract bytecode)

**Account State:**

-   `nonce`: Counter (EOA: tx count, Contract: contracts created)
-   `balance`: ETH balance (Wei = 10^-18 ETH)
-   `storageRoot`: Hash de Merkle Patricia Trie encoding contract storage
-   `codeHash`: Hash de contract code (immutable)

**State Transition:**

Ethereum es state machine. Each block transitions global state:

-   **World State:** Mapping de addresses → account states
-   **Transaction Execution:** Modifies state (balances change, storage updates)
-   **State Root:** Merkle root de world state included in block header

**Transactions:**

```
{
  nonce: 5,
  gasPrice: 20 Gwei,
  gasLimit: 100000,
  to: "0x1234...",  // recipient address (EOA o contract)
  value: 1 ETH,     // ETH to transfer
  data: "0xabc...", // input data (for contract calls)
  v, r, s           // ECDSA signature components
}
```

**Execution:**

1.  Validate signature (recover sender address from signature)
2.  Check nonce (must equal sender's current nonce, prevents replay attacks)
3.  Check balance (sender must have `value + gasLimit * gasPrice`)
4.  Deduct gas fee from sender
5.  Execute transaction:
    -   **If `to` is EOA:** Simple ETH transfer
    -   **If `to` is contract:** Execute contract code with `data` as input
6.  Update state
7.  Refund unused gas

---

### 7.3 Ethereum Virtual Machine (EVM)

**Architecture:**

EVM es stack-based virtual machine que ejecuta smart contract bytecode.

**Stack:**

-   1024 slots max depth
-   Each slot: 256-bit word (optimized for cryptographic operations)
-   Operations pop inputs from stack, push outputs

**Memory:**

-   Volatile (cleared after execution)
-   Byte-addressable
-   Expands as needed (costs gas)

**Storage:**

-   Persistent (survives transaction)
-   Key-value store (256-bit keys → 256-bit values)
-   Expensive (SSTORE opcode costs >20k gas for new storage slot)

**Opcodes:**

EVM has ~140 opcodes:

**Arithmetic:** `ADD`, `SUB`, `MUL`, `DIV`, `MOD`, `EXP`, etc.
**Comparison:** `LT`, `GT`, `EQ`, etc.
**Bitwise:** `AND`, `OR`, `XOR`, `NOT`, `BYTE`, etc.
**Cryptographic:** `SHA3` (Keccak-256), `ECRECOVER` (signature recovery)
**Environmental:** `ADDRESS` (contract address), `CALLER` (msg.sender), `BALANCE`, `TIMESTAMP`, etc.
**Storage:** `SLOAD`, `SSTORE`
**Control Flow:** `JUMP`, `JUMPI` (conditional jump), `STOP`, `RETURN`, `REVERT`, `SELFDESTRUCT`
**Stack:** `PUSH`, `POP`, `DUP` (duplicate), `SWAP`
**Calls:** `CALL` (call another contract), `DELEGATECALL` (execute code in caller's context), `STATICCALL` (read-only call)

**Gas:**

Each opcode costs gas (measured in gas units):

-   Simple operations: `ADD` (3 gas), `MUL` (5 gas)
-   Expensive operations: `SSTORE` (20k gas for new slot, 5k for update, 2.9k refund on delete)
-   External calls: `CALL` (varies, min 700 gas)

**User pays:**
```
Gas Fee = gasUsed * gasPrice
```

**EIP-1559 (Implemented August 2021):**

Restructured fee market:

-   **Base Fee:** Algorithmically adjusted per block (targets 50% full blocks)
    -   Demand high → base fee increases
    -   Demand low → base fee decreases
    -   **Burned** (deflationary)
-   **Priority Fee (Tip):** User-specified tip to validators for inclusion
-   **Max Fee:** Max user willing to pay per gas

**User transaction:**
```
maxFeePerGas = 100 Gwei
maxPriorityFeePerGas = 2 Gwei
baseFee (current) = 50 Gwei

actualFee = min(maxFeePerGas, baseFee + maxPriorityFeePerGas)
          = min(100, 50 + 2) = 52 Gwei per gas

Burned: baseFee * gasUsed
Validator Tip: priorityFee * gasUsed
Refund: (maxFeePerGas - actualFee) * gasUsed
```

**Determinism:**

EVM execution es deterministic: dado same inputs (state, transaction, block context), every node computes identical output.

**Critical para consensus:** Todos nodes must agree on state transitions.

**Turing Completeness:**

EVM es quasi-Turing complete:

-   Supports loops, recursion (unlike Bitcoin Script)
-   **Gas Limit** prevents infinite loops (execution halts cuando gas exhausted)

**Security Considerations:**

**Reentrancy:**

-   Attacker contract calls victim, victim calls back to attacker (re-enters), attacker drains funds before state update
-   **Mitigation:** Checks-Effects-Interactions pattern, ReentrancyGuard (OpenZeppelin)

**Integer Overflow/Underflow:**

-   Arithmetic exceeds 256-bit bounds, wraps around
-   **Mitigation:** Solidity 0.8.0+ has built-in overflow checks; older versions use SafeMath library

**Delegate Call Injection:**

-   `DELEGATECALL` executes code en caller's context (storage)
-   **Attack:** Call malicious library that corrupts your storage
-   **Mitigation:** Only delegatecall to trusted code, use proxies carefully

**Front-Running:**

-   Attacker sees pending transaction in mempool, submits own tx with higher gas price to execute first
-   **Example:** DEX trade, attacker front-runs with buy, back-runs with sell (sandwich attack)
-   **Mitigation:** Flashbots (private mempool), slippage tolerance, commit-reveal schemes

---

### 7.4 Proof of Stake y The Merge

**Pre-Merge: Proof of Work**

Ethereum usó PoW (2015-2022):

-   Mineros compiten solving cryptographic puzzle
-   First to solve proposes block, earns reward (2 ETH post-EIP-1559 + fees + MEV)
-   **Energy Intensive:** ~100 TWh/year (comparable a Netherlands)

**The Merge (Septiembre 15, 2022):**

Ethereum transitioned de PoW a PoS:

-   **Beacon Chain** (consensus layer, PoS, launched Dec 2020) merged con execution layer
-   **Energy Reduction:** ~99.95% (from ~100 TWh/year to ~0.01 TWh/year)
-   **No Change:** EVM, state, transactions unchanged —solo consensus mechanism

**Proof of Stake (Gasper Consensus):**

**Validators:**

-   Stake 32 ETH to become validator
-   Run execution + consensus client
-   Participate in block proposal y attestation
-   Earn rewards: ~4% APR (varies con total staked)

**Epoch y Slot:**

-   **Slot:** 12 seconds (target block time)
-   **Epoch:** 32 slots (6.4 minutes)

**Block Proposal:**

-   Per slot, one validator randomly selected to propose block
-   Propone transactions, broadcast to network

**Attestation:**

-   All validators assigned to committees
-   Attest to validity de proposed block
-   **Attestation:** Vote on head of chain, finality

**Finality:**

-   **Casper FFG (Friendly Finality Gadget):**
    -   Checkpoints every epoch
    -   If 2/3 of validators attest to checkpoint, it becomes "justified"
    -   If next epoch checkpoint justified, previous becomes "finalized"
    -   **Finalized:** Cannot revert (economic finality)

**Fork Choice (LMD GHOST):**

-   **Latest Message Driven Greedy Heaviest Observed Sub-Tree:**
-   If forks exist, follow branch con most attestation weight
-   Ensures convergence even during temporary forks

**Slashing:**

Validators penalized for malicious behavior:

-   **Double Proposal:** Propose two different blocks for same slot
-   **Surround Vote:** Attest conflicting checkpoints
-   **Penalty:** Fraction de stake destroyed, forced exit

**MEV (Maximal Extractable Value):**

**Pre-Merge:** Miners extracted value via:

-   **Front-running:** Insert their transactions before user's
-   **Back-running:** Insert after
-   **Sandwich Attacks:** Front + back
-   **Block Reorganization:** Reorg chain to capture MEV

**Post-Merge:**

-   Validators can still extract MEV
-   **PBS (Proposer-Builder Separation):** Proposed solution separating block construction (builders) from proposal (validators), auctioning blockspace
-   **Flashbots (Flashbots Auction):** Private relay, users submit bundles, builders construct optimal blocks, validators propose, MEV split between parties

---

### 7.5 Soluciones de Escalabilidad (Layer 2)

**El Problema:**

Ethereum mainnet procesa ~15-30 TPS (transactions per second):

-   Insufficient para mass adoption
-   High congestion → high gas fees (in 2021, simple swap cost >$100 gas)

**Solución: Layer 2s**

Procesar transactions off-chain (o en separate chains), settle periódicamente en Ethereum mainnet (L1).

**Categorías:**

**1. Rollups:**

Execute transactions off-chain, post transaction data + state root on-chain.

**Security:** Inherit Ethereum's security (L1 can verify L2).

**Types:**

**Optimistic Rollups:**

**Mechanism:**

-   Assume transactions válidas (optimistic)
-   Post data on-chain (data availability)
-   If fraud, anyone puede submit fraud proof (challenge period: ~7 days)
-   If fraud proven, revert state, slash proposer

**Examples:**

-   **Arbitrum:** Leading Optimistic Rollup, EVM-compatible, many DeFi apps (Uniswap, Aave, GMX)
-   **Optimism:** EVM-compatible, OP token, Optimism Collective (governance experiment)

**Pros:**

-   EVM compatibility (easy to port Ethereum contracts)
-   ~10-100x cheaper than L1

**Cons:**

-   **Withdrawal Delay:** 7-day challenge period to withdraw funds to L1
-   **Data Availability:** Still posts data on-chain (limits scalability vs. ZK rollups)

**ZK-Rollups (Zero-Knowledge Rollups):**

**Mechanism:**

-   Execute transactions off-chain
-   Generate ZK proof (SNARK or STARK) proving correctness
-   Post proof + state root on-chain (tiny data footprint)
-   L1 verifies proof (cryptographically guaranteed validity)

**Examples:**

-   **zkSync Era:** EVM-compatible ZK-rollup, matter labs
-   **StarkNet:** Uses STARKs (different proof system), Cairo programming language (not EVM)
-   **Polygon zkEVM:** EVM-compatible ZK-rollup by Polygon
-   **Scroll:** EVM-compatible ZK-rollup

**Pros:**

-   **Instant Finality:** No challenge period (withdrawals faster than Optimistic)
-   **Higher Scalability:** Less data posted on-chain
-   **Security:** Cryptographic proof (no need trust proposers)

**Cons:**

-   **Complexity:** ZK proof generation computationally intensive
-   **EVM Compatibility:** Harder to achieve (zkEVM development is challenging)
-   **Proving Time:** Currently seconds-minutes to generate proofs (improving with hardware acceleration)

**2. State Channels:**

**Mechanism:**

-   Open channel on-chain (lock funds in multisig)
-   Conduct unlimited transactions off-chain (signed by participants)
-   Close channel on-chain (submit final state)

**Example:**

-   **Lightning Network:** Bitcoin state channels para payments
-   **Raiden:** Ethereum state channels (less adoption)

**Pros:**

-   Instant, free transactions off-chain
-   Perfect for high-frequency interactions entre fixed participants

**Cons:**

-   **Liquidity Locked:** Funds locked durante channel lifetime
-   **Limited Participants:** Channel entre specific parties, no general composability
-   **Complexity:** Channel management, routing payments

**3. Sidechains:**

**Mechanism:**

-   Separate blockchain con own consensus
-   Bridged to Ethereum (tokens locked on L1, minted on sidechain)

**Examples:**

-   **Polygon PoS:** PoS sidechain, high throughput (~7k TPS), low fees, EVM-compatible
-   **Gnosis Chain:** Formerly xDai, PoS sidechain

**Pros:**

-   High throughput
-   EVM compatibility
-   Ecosystem maturity (Polygon has extensive adoption)

**Cons:**

-   **Separate Security:** Does NOT inherit Ethereum security (own validator set)
-   **Bridge Risk:** Bridges vulnerable to hacks (billions lost in bridge exploits)

**4. Validiums:**

Like ZK-rollups but data availability off-chain.

**Example:** StarkEx (powers dYdX, Immutable X)

**Pros:**

-   Extreme scalability (no data on-chain)

**Cons:**

-   **Data Availability Risk:** If off-chain data withheld, users can't prove ownership
-   **Trust Assumption:** Must trust data availability committee

**Comparison:**

| Solution          | Finality       | Withdrawal | Security        | Scalability  | EVM       |
| ----------------- | -------------- | ---------- | --------------- | ------------ | --------- |
| Optimistic Rollup | ~7 days        | ~7 days    | Ethereum        | ~10-100x     | Yes       |
| ZK-Rollup         | Fast           | Fast       | Ethereum        | ~100-1000x   | Developing |
| State Channel     | Instant        | Instant    | Participants    | Infinite     | N/A       |
| Sidechain         | Fast           | Fast       | Own             | High         | Yes       |
| Validium          | Fast           | Fast       | ZK (data trust) | Extreme      | Varies    |

**Ethereum Roadmap (Post-Merge):**

**The Surge:** Achieve 100k+ TPS via L2s, proto-danksharding (EIP-4844), full danksharding

**EIP-4844 (Implemented March 2024):**

-   **Blob Transactions:** New transaction type carrying "blobs" de data (temporary, deleted after ~1 month)
-   **Purpose:** Cheap data availability para rollups
-   **Impact:** Reduce L2 costs ~10x

**Full Danksharding (Future):**

-   Increase blob capacity massively
-   Target: 16 MB/block (vs. current ~128 KB blobs)
-   Enable millions of TPS across rollups

**Data Availability Sampling (DAS):**

-   Light nodes can verify data availability without downloading all blobs
-   Critical para scalability manteniendo decentralization
