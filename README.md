# 🆔 IDChain – Decentralized Digital Identity for Informal Workers

**IDChain** is a decentralized identity platform built on the Internet Computer Protocol (ICP) that empowers informal workers—such as gig drivers, street vendors, and daily laborers—to obtain a verifiable digital identity. This enables access to microfinance, government aid, and cross-platform verification services without traditional bureaucracy.

---

## 🎯 Project Goals

- Provide valid, verifiable digital identity (KTP-ICP) for informal workers using SSI principles.
- Facilitate microloans and social assistance eligibility checks with on-chain verification.
- Eliminate manipulation and inefficiencies in identity data collection and aid distribution.
- Ensure portability across Web3 applications without repeated user registration.

---

## 🛠 Tech Stack

### Frontend
- **React.js**
- **TailwindCSS**
- **Plug Wallet SDK** / Internet Identity (II)
- `@dfinity/agent` for canister communication

### Backend (Canisters)
- **Motoko**
- **DFX** (ICP SDK for local and mainnet deployment)
- **StableHeapBTreeMap** (imported via MOPS manually)

---

## 🔐 Key Features

| Feature                      | Description                                                                 |
|-----------------------------|-----------------------------------------------------------------------------|
| 🪪 Identity Registration     | Users upload encrypted e-KTP and selfie data via a secure front-end         |
| 🏛 Government Oracle Signing | Official personnel verify and sign user data manually                      |
| ✅ On-chain Verification     | Status `Verified_KTP` stored securely and read-only accessible              |
| 🔁 Cross-app Portability     | Apps can check `Verified` status without needing to store user data         |
| 💸 Financial Access Layer   | Enables Cash Social assistance apps, cooperatives, and P2P fintech to validate eligibility  |
| 👛 Wallet Integration        | Plug wallet + token support for balance, aid, and micro-credit              |

---

## 🧱 Canister Architecture

### `IdentityVault.mo`
- Stores encrypted user identity records
- Functions:
  - `registerIdentity()`
  - `getVerificationStatus()`
  - `verifyByOracle()`

### `OracleSignature.mo`
- Designed for use by authorized government officials (Disdukcapil/Social Dept)
- Functions:
  - `signIdentity()` – signs user hash
- Private keys are cold-stored off-chain; only public keys are used on-chain

---

## 🧩 Application Flow

1. **User Registration**
   - Connect Plug Wallet / Internet Identity
   - Upload e-KTP file + selfie photo + optional documents
   - Data is hashed, encrypted, and stored on-chain

2. **Manual Verification by Oracle**
   - Verified by government officer (in-person document checks)
   - Officer signs identity hash using `OracleSignature` canister

3. **Verified Status Stored**
   - `Verified_KTP` status is saved on-chain
   - Readable by third-party apps (e.g. bansos, microloan apps)

4. **Financial & Social Program Integration**
   - Bansos portals can check status for automated eligibility
   - Microfinance apps can use on-chain data for fast loan approvals
   - Additional loan records stored in future `LoanLedger` smart contract

---
## 📦 Installation & Development

### 1. Clone Repository
```bash
git clone https://github.com/yourname/idchain.git
cd idchain
```

### 2. Setup Frontend
```bash
cd frontend
npm install
npm run dev
```
This will start the React development server. Open your browser at `http://localhost:3000` to view the app.

### 3. Setup Motoko Dependencies
```bash
cd backend
mops add https://github.com/canscale/StableHeapBTreeMap
mops install
```
> **Note:** The `mops` tool is used to manage Motoko packages. If you don’t have it installed, you can get it from [MOPS GitHub](https://github.com/dfinity/motoko-packages).

### 4. Start ICP Local Replica and Deploy Canisters
```bash
dfx start --background
dfx deploy
```
This will start a local Internet Computer replica and deploy all canisters.

### 5. Running the Full Application
- Make sure both backend canisters and frontend are running.
- Connect your wallet (Plug Wallet or Internet Identity).
- Register identity, and proceed with the verification flow.

---

## 👥 Team

| Member | Role                                |
|--------|-------------------------------------|
| Alfian | Team Lead / Integration Engineer    |
| Hanif  | Identity & Backend Architect        |
| Razi   | Field Research / Use Case Modeling  |
| Haris  | UI/UX Designer & Frontend Developer |

---

## 📄 License

MIT License – Free for use in social, research, and hackathon projects.

---

Please submit pull requests or open issues for discussion at [GitHub Issues](https://github.com/alfianramadani/idchain/issues).
