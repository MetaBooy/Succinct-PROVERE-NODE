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
```
Restart your PC.

2. Download Docker Desktop
Go to: [LINK](https://www.docker.com/products/docker-desktop/)

Click Download for Windows and install it.

## 3. Enable WSL2 Integration
After installation:

Open Docker Desktop

Go to Settings > General

Ensure "Use WSL 2 instead of Hyper-V" is checked

Go to Settings > Resources > WSL Integration and enable for your distro (e.g., Ubuntu)


## 4. (Optional) Enable GPU Support
If you want to run GPU containers:

✅ Make sure:

You have NVIDIA driver + CUDA installed

You install NVIDIA Container Toolkit inside WSL2 Ubuntu

In WSL2 Ubuntu terminal:
```sudo apt update && sudo apt install -y nvidia-container-toolkit
sudo systemctl restart docker
```

## 5. Test Docker
In a terminal (Command Prompt, PowerShell, or Ubuntu):
```docker --version
docker run hello-world
```


## If you installed with Docker, you can run the following command:

```docker run --rm public.ecr.aws/succinct-labs/spn-node:latest-gpu calibrate \
    --usd-cost-per-hour 0.80 \
    --utilization-rate 0.5 \
    --profit-margin 0.1 \
    --prove-price 1.00
```

**This will output calibration results that look like the following:**

### Parameters

| Parameter        | Value  |
|------------------|--------|
| Cost Per Hour    | $0.80  |
| Utilization Rate | 50.00% |
| Profit Margin    | 10.00% |
| Price of $PROVE  | $1.00  |



Starting calibration...

### Calibration Results

| Metric               | Value                   |
|----------------------|-------------------------|
| Estimated Throughput | 1742469 PGUs/second     |
| Estimated Bid Price  | 0.28 $PROVE per 1B PGUs |


**This tells you that your prover can prove 1742469 prover gas units (PGUs) per second and that you should bid 0.28 $PROVE per 1B PGUs for proofs.**

## Set these parameters as environment variables for later use:

```export PGUS_PER_SECOND=<PGUS_PER_SECOND>
export PROVE_PER_BPGU=<PROVE_PER_BPGU>
export PROVER_ADDRESS=<PROVER_ADDRESS>
export PRIVATE_KEY=<PRIVATE_KEY>
```

## Step 5: Run the Prover
At this point, we've done all the necessary setup. If you installed with Docker, you can run the following command:

```docker run --rm public.ecr.aws/succinct-labs/spn-node:latest-gpu prove \
    --rpc-url https://rpc-production.succinct.xyz \
    --throughput $PGUS_PER_SECOND \
    --bid $PROVE_PER_BPGU \
    --private-key $PRIVATE_KEY \
    --prover $PROVER_ADDRESS
```
**EXAMPLE**
```docker run --rm public.ecr.aws/succinct-labs/spn-node:latest-gpu prove \
    --rpc-url https://rpc-production.succinct.xyz \
    --throughput 1742469 \
    --bid 0.28 \
    --private-key ecb2bca32ceccddd250a8d350000000000000e0cbed7f9fe4d4a \
    --prover 0x52CB34919E71Df2615045e7b58dD5cea9F720b20
```


## DODE YOUR PROVER NODE RUNING

**What hardware is recommended for running a prover?**
The minimal implementation works on standard consumer hardware, but competitive provers typically use optimized setups with powerful GPUs. As a reminder, most competitive provers use high-end GPUs like NVIDIA 4090s and orchestrate their own proving software to maximize throughput.



