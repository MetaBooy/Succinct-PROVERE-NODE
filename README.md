# 🧠 Succinct Prover Node Setup (WSL2 + Docker + GPU Ready)
# Step 1: Requirements
You will need a fresh Ethereum wallet with some Sepolia ETH to interact with protocol smart contracts. We suggest using a fresh wallet for this purpose since the private key will be used inside the proving CLI.

You will also need at least 1000 $PROVE tokens to stake to your prover. You can obtain these tokens through faucet.(https://docs.google.com/forms/d/e/1FAIpQLSfgTpBL_wMWyyoxT6LxuMhiu-bex0cBg9kRTmxoKw3XOluOCA/viewform)

# Step 2: Create Your Prover
To create a prover, you need to call createProver(uint256 _stakerFeeBips) on the SuccinctStaking contract. (https://staking.sepolia.succinct.xyz/prover)

We suggest doing this through our frontend here. You can also interact with the contract directly using cast, Etherscan, or a similar tool.

By default, the wallet you use to create the prover will be the owner of the prover and also the delegated signer used to sign transactions on behalf of the prover.

Remember the address of the prover you created (not the same as the wallet that created it). You will need it later.

Step 3: Stake to Your Prover
The next step is to stake to your prover. You can do this by calling the stake(address _prover, uint256 _amount) function on the SuccinctStaking contract.

We also suggest doing this through our frontend here. Similarly, you can also interact with the contract directly using cast, Etherscan, or a similar tool.



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

## 🚀 **1. Install WSL2 + Ubuntu**
'''sudo apt update
sudo apt install docker.io -y
sudo usermod -aG docker $USER
newgrp docker


# **3. Enable GPU for Docker (Optional: RTX 4060)**
Install NVIDIA Toolkit:
'''distribution=$(. /etc/os-release;echo $ID$VERSION_ID)
curl -s -L https://nvidia.github.io/libnvidia-container/gpgkey | sudo apt-key add -
curl -s -L https://nvidia.github.io/libnvidia-container/$distribution/libnvidia-container.list | sudo tee /etc/apt/sources.list.d/nvidia-container-toolkit.list

sudo apt update
sudo apt install -y nvidia-container-toolkit
sudo service docker restart

# **4. If you installed with Docker, you can run the following command:**
'''docker run --rm public.ecr.aws/succinct-labs/spn-node:latest-gpu calibrate \
    --usd-cost-per-hour 0.80 \
    --utilization-rate 0.5 \
    --profit-margin 0.1 \
    --prove-price 1.00

This will output calibration results that look like the following:

Parameters:
┌──────────────────┬────────┐
│ Parameter        │ Value  │
├──────────────────┼────────┤
│ Cost Per Hour    │ $0.80  │
├──────────────────┼────────┤
│ Utilization Rate │ 50.00% │
├──────────────────┼────────┤
│ Profit Margin    │ 10.00% │
├──────────────────┼────────┤
│ Price of $PROVE  │ $1.00  │
└──────────────────┴────────┘

Starting calibration...

Calibration Results:
┌──────────────────────┬─────────────────────────┐
│ Metric               │ Value                   │
├──────────────────────┼─────────────────────────┤
│ Estimated Throughput │ 1742469 PGUs/second     │
├──────────────────────┼─────────────────────────┤
│ Estimated Bid Price  │ 0.28 $PROVE per 1B PGUs │
└──────────────────────┴─────────────────────────┘

This tells you that your prover can prove 1742469 prover gas units (PGUs) per second and that you should bid 0.28 $PROVE per 1B PGUs for proofs.

Set these parameters as environment variables for later use:

'''export PGUS_PER_SECOND=<PGUS_PER_SECOND>
export PROVE_PER_BPGU=<PROVE_PER_BPGU>
export PROVER_ADDRESS=<PROVER_ADDRESS>
export PRIVATE_KEY=<PRIVATE_KEY>

# **Step 5: Run the Prover**
At this point, we've done all the necessary setup. If you installed with Docker, you can run the following command:

'''docker run --rm public.ecr.aws/succinct-labs/spn-node:latest-gpu prove \
    --rpc-url https://rpc-production.succinct.xyz \
    --throughput $PGUS_PER_SECOND \
    --bid $PROVE_PER_BPGU \
    --private-key $PRIVATE_KEY \
    --prover $PROVER_ADDRESS
# **example of this**
'''sudo docker run --rm public.ecr.aws/succinct-labs/spn-node:latest-gpu prove \
  --rpc-url https://rpc-production.succinct.xyz \
  --throughput 1742469 \
  --bid 0.28 \
  --private-key ecb2bca32ce0000050a80000001ffe0cbed7f9fe4d4a \
  --prover 0x52CB34919E71Df2615045e7b58dD5cea9F720b20
