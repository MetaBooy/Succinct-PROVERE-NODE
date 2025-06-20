# Step 1: Requirements
You will need a fresh Ethereum wallet with some Sepolia ETH to interact with protocol smart contracts. We suggest using a fresh wallet for this purpose since the private key will be used inside the proving CLI


You will also need at least 1000 $PROVE tokens to stake to your prover. You can obtain these tokens through [FAUCET](https://docs.google.com/forms/d/e/1FAIpQLSfgTpBL_wMWyyoxT6LxuMhiu-bex0cBg9kRTmxoKw3XOluOCA/viewform)

# Step 2: Create Your Prover

Create Your Prover GO THIS [LINK](https://staking.sepolia.succinct.xyz/prover) AND STAKE 1000 $PROVE TOKEN

# Step 4: Calibrate the Prover
The prover needs to be calibrated to your hardware in order to configure key parameters that govern its behavior. There are two key parameters that need to be set:

Bidding Price: This is the price per proving gas unit (PGU) that the prover will bid for. This determines the profit margin of the prover and it's competitiveness with the rest of the network.
Expected Throughput: This is an estimate of the prover's proving throughput in PGUs per second. This is used to estimate whether a prover can complete a proof before its deadline.


# 🧠 Succinct Prover Node Setup (WSL2 + Docker + GPU Ready)

Run a Succinct Prover Node on a **Windows PC** with **WSL2 + Ubuntu**, **Docker**, and **RTX 4060 (GPU)** support.

---

## 📦 Requirements

- Windows 10/11
- WSL2 + Ubuntu
- Docker
- NVIDIA GPU (optional, for proving acceleration)
- Testnet $PROVE tokens (optional for bidding)

---

## 🚀 1. Install WSL2 + Ubuntu

Open PowerShell as Admin:

```powershell
wsl --install



### 🐳 2. Install Docker inside WSL (Ubuntu)

```sudo apt update
sudo apt install docker.io -y
sudo usermod -aG docker $USER
newgrp docker



