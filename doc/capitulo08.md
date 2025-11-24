Aquí tienes el Capítulo 8.

---

## Capítulo 8: Sistemas Económicos: DeFi y Criptomonedas

### 8.1 Finanzas Descentralizadas (DeFi)

**Definición:**

DeFi (Decentralized Finance) recrea servicios financieros tradicionales —lending, trading, derivatives, insurance— usando smart contracts en blockchain sin intermediarios centralizados.

**Principios Clave:**

1.  **Non-Custodial:** Users retain control de sus assets (not your keys, not your coins)
2.  **Permissionless:** Anyone con wallet puede access
3.  **Transparent:** All transactions, código visible on-chain
4.  **Composable:** Protocols interoperate ("money legos")
5.  **Programmable:** Logic encoded en smart contracts

**Total Value Locked (TVL):**

Métrica key para DeFi: total value depositada en protocols.

-   **Peak (Nov 2021):** ~$180B
-   **Bear Market (2022-2023):** Dropped to ~$40B post-Terra/Luna collapse, FTX implosion
-   **Recovery (2024-2025):** ~$100B (aproximado, fluctúa)

**Major DeFi Categories:**

**1. Decentralized Exchanges (DEXs):**

Trade crypto without centralized exchange (Coinbase, Binance).

**Automated Market Makers (AMMs):**

Replace order book con liquidity pools.

**Uniswap:**

-   Most dominant DEX (~$4B daily volume)
-   **V2:** Constant Product Market Maker (`x * y = k`)
-   **V3:** Concentrated Liquidity (LPs choose price ranges for capital efficiency)
-   **V4 (Coming):** Hooks (customizable pool logic), optimized gas

**Curve:**

-   Specialized para stablecoin swaps
-   Low slippage entre similar-priced assets
-   Large liquidity pools (3pool: DAI/USDC/USDT ~$2B TVL)

**Balancer:**

-   Customizable pools (not just 50/50 split), weighted pools, stable pools
-   Pool as index fund

**Other:** SushiSwap (Uniswap fork), PancakeSwap (Binance Smart Chain), 1inch (aggregator)

**2. Lending Protocols:**

Borrow/Lend crypto assets, earn interest.

**Aave:**

-   **TVL:** ~$10B
-   **Mechanism:**
    -   Deposit assets → earn interest (variable APY based on utilization)
    -   Borrow against collateral (overcollateralized: deposit $150 ETH, borrow $100 USDC)
    -   Algorithmically determined interest rates
    -   Flash Loans: Borrow uncollateralized within single transaction (pay back or revert)

**Compound:**

-   Similar architecture (cTokens instead of aTokens)
-   Governance via COMP token
-   Pioneered "liquidity mining" (2020)

**Maker (MakerDAO):**

-   Decentralized stablecoin issuer (DAI)
-   Deposit collateral (ETH, wBTC, stablecoins) → mint DAI
-   Governance via MKR token
-   **Peg Stability Module (PSM):** 1:1 swap USDC<->DAI para tight peg

**3. Derivatives:**

**Synthetix:**

-   Synthetic assets tracking real-world prices (sUSD, sBTC, commodities, indices)
-   SNX stakers collateralize debt pool, mint synths
-   Stakers earn fees, take on debt pool risk

**dYdX:**

-   Decentralized perpetual futures exchange
-   **V3:** StarkEx (validium), high performance
-   **V4 (Cosmos-based):** Separate blockchain, order book

**GMX:**

-   Decentralized perpetual exchange on Arbitrum, Avalanche
-   GLP pool provides liquidity (users trade against pool)
-   Up to 50x leverage

**4. Stablecoins:**

(Detallado en 8.4)

**5. Yield Aggregators:**

**Yearn Finance:**

-   Auto-compound yield strategies
-   Vaults deposited assets, strategies harvest rewards, compound
-   Governance via YFI token

**6. Insurance:**

**Nexus Mutual:**

-   Decentralized insurance para smart contract risk
-   Members stake capital, vote on claims
-   **Cover:** Purchase coverage for specific protocols

---

### 8.2 Bitcoin: Dinero Digital Descentralizado

**Genesis:**

-   **Whitepaper:** Satoshi Nakamoto, octubre 2008: "Bitcoin: A Peer-to-Peer Electronic Cash System"
-   **Genesis Block:** Enero 3, 2009 ("The Times 03/Jan/2009 Chancellor on brink of second bailout for banks")

**Design:**

**1. Fixed Supply:**

-   **Maximum:** 21 million BTC
-   **Halving:** Block reward halves every 210,000 blocks (~4 years)
    -   2009-2012: 50 BTC/block
    -   2012-2016: 25 BTC/block
    -   2016-2020: 12.5 BTC/block
    -   2020-2024: 6.25 BTC/block
    -   2024-2028: 3.125 BTC/block
    -   ...
    -   ~2140: Last BTC mined, thereafter solo transaction fees

**2. Proof of Work:**

-   SHA-256 hash puzzle
-   Difficulty adjusts every 2016 blocks (targeting 10 min/block)
-   **Hash Rate:** ~400 EH/s (exahashes/sec, 2024)

**3. UTXO Model:**

Unlike Ethereum's account model, Bitcoin usa Unspent Transaction Outputs:

-   Each transaction consumes UTXOs (inputs), creates new UTXOs (outputs)
-   Analogy: cash denominations (consume $20 bill, receive $15 + $5 change)

**4. Scripting Language:**

-   Not Turing-complete (no loops)
-   **Script:** Stack-based language para transaction conditions
-   **Common Scripts:**
    -   **P2PKH (Pay to Public Key Hash):** Standard payment
    -   **P2SH (Pay to Script Hash):** Multisig, complex conditions
    -   **P2WPKH (SegWit):** Witness segregation, lower fees
    -   **P2TR (Taproot, 2021):** Enhanced privacy, complex scripts look like standard txs

**Narratives:**

**1. Digital Gold:**

-   Scarce (21M cap)
-   Store of value, inflation hedge
-   Not controlled by any government
-   "Hard money" (Austrian economics)

**2. Censorship-Resistant Money:**

-   No one can freeze your Bitcoin (if you control keys)
-   Cross-border payments without permission
-   Escape capital controls, oppressive regimes

**3. Settlement Layer:**

-   Layer 1 (Bitcoin base layer) for high-value final settlement
-   Layer 2 (Lightning Network) para micro-payments

**Criticisms:**

**1. Volatility:**

-   Price swings ±20% semanas, ±50% años
-   Poor medium of exchange (quien gasta algo que puede 2x next month?)
-   Store of value debatable durante bear markets

**2. Energy Consumption:**

-   ~150 TWh/año (~0.5% global electricity)
-   **Defense:** Can use renewable energy, incentivizes cheap/excess energy
-   **Criticism:** Regardless of energy source, opportunity cost, environmental impact

**3. Scalability:**

-   Base layer: ~7 TPS (vs. Visa ~24k TPS)
-   Transaction fees spike durante alta demanda
-   **Lightning Network** promises scaling pero adoption limitada, UX challenges

**4. Limited Programmability:**

-   Not smart contract platform
-   Cannot build DeFi natively (necesita layers como RSK o wrapped BTC en Ethereum)

**Bitcoin en DI Q SOCIENTAS:**

**Role:** Monetary base layer, reserve asset.

-   DAOs pueden hold BTC en treasuries
-   Cross-border payments sin intermediarios
-   Hedge contra fiat inflation

**Limitation:** Limited utility para complex organizational/financial logic (DAOs, DeFi) —requiere Ethereum o otras platforms.

---

### 8.3 Ether y el Ecosistema Ethereum

**Ether (ETH):**

Native asset de Ethereum blockchain.

**Functions:**

1.  **Gas Payment:** Transactions require ETH para pay gas fees
2.  **Staking:** Validators stake 32 ETH para participate en consensus
3.  **Collateral:** Used en DeFi (Aave, MakerDAO) como collateral
4.  **Medium of Exchange:** Trade para other tokens
5.  **Store of Value:** (debatable, more volatile than BTC)

**Monetary Policy:**

**Pre-Merge:**

-   **Issuance:** ~4.5% anual (PoW mining rewards)
-   **Inflationary:** Increasing supply

**Post-Merge (Septiembre 2022):**

-   **Issuance:** ~0.5% anual (PoS validator rewards, much lower)
-   **EIP-1559 Burn:** Base fee burned (deflationary pressure)
-   **Net:** Depends on transaction demand
    -   High demand (many transactions) → high burn → **deflationary**
    -   Low demand → low burn → **slightly inflationary**

**Ultrasound Money:**

Narrative post-Merge: ETH más deflationary que BTC (if demand sufficient).

**Supply:**

-   **Current:** ~120M ETH (fluctuates con burn)
-   **No cap:** Unlike Bitcoin, sin fixed maximum

**Debate:** Should Ethereum have supply cap? Vitalik Buterin has considered, pero no consensus.

**ETH as Investment:**

**Bull Case:**

-   Ethereum es infraestructura para DeFi, NFTs, Web3
-   Network effects, developer dominance
-   PoS staking yield (~4%) atrae capital
-   Deflationary if activity high
-   "Ultrasound money" narrative

**Bear Case:**

-   Competition from faster L1s (Solana, Avalanche)
-   Centralization concerns (Lido dominates staking)
-   Regulatory risk (ETH treated as security?)
-   High L1 fees persist despite L2s (UX friction)

**Staking:**

**Solo Staking:**

-   Run own validator node (32 ETH)
-   Earn rewards, contribute to decentralization
-   **Barriers:** Technical expertise, hardware, uptime requirements

**Staking Pools:**

-   **Lido:** Largest (dominates ~30% of staked ETH)
-   Stake any amount, receive stETH (liquid staking token)
-   **Risk:** Centralization (Lido controls many validators)

**Centralized Exchanges:**

-   Coinbase, Binance offer staking services
-   Custodial (trust exchange con keys)

---

### 8.4 Stablecoins: El Puente Crítico

Stablecoins are crypto-assets designed to maintain stable value (typically pegged 1:1 to USD).

**Why Critical:**

1.  **Medium of Exchange:** Stable value makes viable for payments
2.  **Unit of Account:** Price goods/services en stablecoins
3.  **DeFi Backbone:** Most DeFi liquidity en stablecoin pairs
4.  **Bridge Fiat-Crypto:** Entry/exit ramp between worlds
5.  **Remittances:** Low-cost cross-border transfers

**Types:**

**1. Fiat-Collateralized:**

Backed 1:1 by fiat reserves (USD en bank accounts or Treasuries).

**USDC (USD Coin):**

-   **Issuer:** Circle (fintech co.)
-   **Market Cap:** ~$35B (fluctuates)
-   **Reserves:** Cash + short-term US Treasuries (monthly attestations by Grant Thornton, auditor)
-   **Regulatory:** Compliant con regulations, banking partnerships
-   **Centralized:** Circle can freeze/blacklist addresses
-   **Redemption:** 1 USDC always redeemable for 1 USD (if KYC'd)

**USDT (Tether):**

-   **Issuer:** Tether Limited (Bitfinex-affiliated)
-   **Market Cap:** ~$100B (largest stablecoin)
-   **Reserves:** Historically opaque, improved transparency (quarterly attestations)
    -   Mix de cash, Treasuries, commercial paper, other assets
    -   **Controversy:** Never fully audited, questions sobre reserves adequacy
-   **Dominant:** Widely used en centralized exchanges, high liquidity
-   **Centralized:** Can freeze addresses

**2. Crypto-Collateralized:**

Backed by crypto assets (overcollateralized para absorb volatility).

**DAI (MakerDAO):**

-   **Market Cap:** ~$5B
-   **Mechanism:**
    -   Users deposit collateral (ETH, wBTC, USDC, etc.) en Maker Vault
    -   Mint DAI (stablecoin) up to collateralization ratio (e.g., 150%)
    -   **Example:** Deposit $150 ETH, mint $100 DAI
    -   Pay stability fee (interest) on DAI debt
-   **Decentralized:** No central issuer
-   **Governance:** MKR token holders vote on parameters (collateral types, ratios, fees)
-   **Peg Mechanism:**
    -   If DAI < $1: Increase DSR (DAI Savings Rate) → incentivize hold/buy → price up
    -   If DAI > $1: Decrease stability fee → incentivize mint → supply up, price down
    -   **PSM (Peg Stability Module):** 1:1 swap USDC<->DAI (tightens peg, controversial because centralizes reliance on USDC)
-   **Liquidation:** If collateral value drops below threshold, vault liquidated (collateral auctioned)

**3. Algorithmic (Mostly Failed):**

Attempt to maintain peg via algorithm without full collateral.

**UST/Terra (Collapsed Mayo 2022):**

-   **Mechanism:** UST stablecoin paired with LUNA (volatile token)
    -   Mint 1 UST by burning $1 worth of LUNA
    -   Redeem 1 UST for $1 worth of LUNA
    -   **Peg:** Arbitrage keeps UST near $1
        -   If UST < $1: Buy UST, redeem for $1 LUNA, sell LUNA → profit + push UST up
        -   If UST > $1: Mint UST con LUNA, sell UST → profit + push UST down
-   **Anchor Protocol:** Offered 20% APY on UST deposits (unsustainable yield)
-   **Death Spiral (May 2022):**
    -   Large UST sell pressure (panic, redemptions)
    -   UST de-pegs below $1
    -   Massive LUNA minting to redeem UST → hyperinflation de LUNA
    -   LUNA price crashes → further undermines UST confidence → more redemptions → spiral
    -   Result: ~$40B value destruction, LUNA goes to ~zero, UST collapses
-   **Lesson:** Algorithmic stablecoins sin adequate collateral are fragile, prone to death spirals

**Other Algorithmic Attempts:**

-   **FRAX:** Fractional-algorithmic (partial collateral), survived Terra collapse
-   **RAI (Reflexer):** Floating peg (not $1), purely crypto-collateralized

**Regulatory Landscape:**

**Key Concerns:**

1.  **Runs:** If confidence lost, rapid redemptions could destabilize (Terra example)
2.  **Reserves:** Are reserves actually 1:1? (Tether controversies)
3.  **Systemic Risk:** If major stablecoin collapses, contagion to DeFi
4.  **Money Transmitter:** Stablecoins may be subject to banking/money transmitter regulations

**U.S.:**

-   **No Federal Framework Yet:** Proposed legislation (stablecoin bills) en Congress, no enactment
-   **State Level:** Some states require money transmitter licenses
-   **SEC:** Could classify some stablecoins as securities

**E.U. (MiCA):**

-   **E-Money Tokens (EMTs):** Fiat-backed stablecoins
-   **Requirements:** Reserve 1:1, redemption rights, authorization/licensing

**Centralization Concerns:**

Circle (USDC), Tether (USDT) can:

-   **Freeze Addresses:** Blacklist wallets (e.g., sanctions compliance)
-   **Control Reserves:** Trust that reserves exist
-   **Redeem Selectively:** KYC/AML for redemptions

**Tension:** Stablecoins offer DeFi efficiency pero centralized stablecoins undermine decentralization ethos.

**Ideal:** Decentralized, scalable, stable. **Reality:** Pick two (trilemma).

---

### 8.5 CBDCs: Dinero Digital Estatal

**Central Bank Digital Currencies (CBDCs):** Digital version de fiat currency issued by central bank.

**Motivation:**

1.  **Financial Inclusion:** Unbanked can access digital payments without commercial bank account
2.  **Payment Efficiency:** Instant settlement, lower costs vs. traditional banking
3.  **Monetary Policy:** Direct distribution (helicopter money), negative interest rates más feasible
4.  **Counter Crypto:** Compete con private stablecoins, criptomonedas
5.  **Anti-Crypto:** Easier monitoring, control vs. pseudonymous crypto

**Types:**

**1. Retail CBDC:**

-   Directly accessible by citizens/businesses
-   Replace cash digitally
-   **Example (Piloted):** e-CNY (China), Sand Dollar (Bahamas), eNaira (Nigeria)

**2. Wholesale CBDC:**

-   Inter-bank settlements
-   Not accessible by public
-   **Example:** Project Helvetia (Swiss National Bank)

**Design Choices:**

**Account-Based vs. Token-Based:**

-   **Account:** Balance en central bank account (like traditional banking)
-   **Token:** Bearer instrument (like cash), transferable peer-to-peer

**Centralized vs. Distributed Ledger:**

-   **Centralized Database:** Central bank controls (like traditional banking infrastructure)
-   **DLT (Blockchain):** Distributed among authorized nodes (permissioned blockchain)

**Privacy:**

-   **Full Anonymity:** Like cash
-   **Full Surveillance:** Central bank sees all transactions
-   **Middle Ground:** Tiered privacy (small amounts anonymous, large amounts tracked)

**Interest Bearing:**

-   **Non-Interest Bearing:** Like cash
-   **Interest Bearing:** Competes with bank deposits (could disintermediate commercial banks)

**Case Studies:**

**China (e-CNY / Digital Yuan):**

-   Most advanced large-scale CBDC
-   **Pilots:** Multiple cities, millions users, billions transactions
-   **Design:** Centralized, account-based, tiered privacy, non-interest bearing
-   **Wallet:** e-CNY app (controlled by People's Bank of China)
-   **Use Cases:** Retail payments, government salaries, subsidies
-   **Concerns:**
    -   **Surveillance:** Government can track all transactions
    -   **Control:** Can freeze/control wallets
    -   **Weaponization:** Social credit system integration fears

**Bahamas (Sand Dollar):**

-   Launched October 2020 (first nationwide CBDC)
-   **Motivation:** Financial inclusion para remote islands
-   **Adoption:** Limited, usage low
-   **Challenge:** Merchant acceptance, user inertia

**Nigeria (eNaira):**

-   Launched October 2021
-   **Goal:** Financial inclusion, reduce cash dependence
-   **Adoption:** Extremely low (~0.5% population after 1 year)
-   **Issues:** Lack of trust, preference for cash y mobile money (M-Pesa style)

**European Central Bank (Digital Euro):**

-   **Investigation Phase:** Research ongoing, decision expected ~2025
-   **Design:** Retail, emphasis on privacy protections (relative), offline capability
-   **Concerns:** Bank disintermediation, ECB becomes retail banker?
-   **Timeline:** If approved, launch ~2028+

**Federal Reserve (U.S.):**

-   **Cautious:** Research, no concrete plans
-   **Discussion Paper (2022):** Pros/cons, public feedback
-   **Political Resistance:** Republicans wary de surveillance, Democrat support mixed
-   **Alternatives:** Private stablecoins (USDC) de facto function as digital dollar

**CBDCs vs. Crypto:**

| Feature               | CBDC                                   | Decentralized Crypto          |
| --------------------- | -------------------------------------- | ----------------------------- |
| Issuer                | Central Bank                           | Algorithmic/Protocol          |
| Centralization        | Fully Centralized                      | Decentralized                 |
| Privacy               | Low-Medium (surveillance possible)     | Medium-High (pseudonymous)    |
| Programmability       | Limited (policy constraints)           | High (smart contracts)        |
| Permissionless        | No (controlled access)                 | Yes (open access)             |
| Censorship Resistance | No (central control)                   | High                          |
| Stability             | Stable (fiat-backed)                   | Variable (crypto volatility)  |

**DI Q SOCIENTAS Perspective:**

**Concerns:**

-   **Surveillance State:** CBDCs enable total financial surveillance, undermining privacy
-   **Control:** Governments can freeze assets, enforce negative interest, program money (expiration dates, restricted uses)
-   **Disintermediation:** Could replace commercial banks, concentrate power en central bank
-   **Threat to Crypto:** CBDCs positioned as "safe" alternative, regulations could favor CBDCs over decentralized crypto

**Potential Benefits:**

-   **Financial Inclusion:** If designed well, can bank unbanked
-   **Efficiency:** Faster, cheaper payments
-   **Interoperability:** If CBDCs interoperable con blockchain tech, could bridge TradFi-DeFi

**Hybrid Future:**

-   **Coexistence:** CBDCs para everyday payments (stable, trusted), decentralized crypto para savings, censorship resistance, programmable finance
-   **Competition:** Private stablecoins (USDC, DAI) compete con CBDCs
-   **Complementarity:** CBDCs settle on blockchain rails, integrate con DeFi

**NEBUAH Position:**

-   **Advocacy:** Push para privacy-preserving CBDC designs (tiered privacy, anonymity for small transactions)
-   **Interoperability:** Promote standards para CBDC-DeFi bridges
-   **Education:** Inform public sobre privacy risks, importance de preserving decentralized alternatives
-   **Pluralism:** Support multi-currency ecosystem (CBDCs + private stablecoins + decentralized crypto coexist)
