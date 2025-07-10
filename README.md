# **Running a Succinct Prover Node on Sepolia**

Welcome to the Succinct Prover Network node instructions! Here, you’ll find everything you’ll need to run a prover on the network. We’ve made it really simple for you to participate: all you have to do is stake testnet PROVE tokens and run a script.

## **1. Setup your GPU**

Make sure your machine has these specs: 

- **GPU:** NVIDIA RTX 3090 or 4090
- **Memory: 24 GB RAM (required)**
- **Disk: 100 GB (recommended)**
- **CPU: 4 cores (required)**
- **Template: Ubuntu VM (22.04/24.04) (required)**

You can rent a machine at any of these providers:

- **Genesis Cloud:** ~$0.2/hr. Easy setup. Username: ubuntu. Password given during checkout. https://www.genesiscloud.com/pricing
- **TensorDock:** RTX 3090/4090. https://dashboard.tensordock.com/deploy
- **Vast.ai:** https://cloud.vast.ai/?gpu_option=RTX%203090

## **2. Get $PROVE on Ethereum Sepolia**

Fill out this [form](https://docs.google.com/forms/d/e/1FAIpQLSfgTpBL_wMWyyoxT6LxuMhiu-bex0cBg9kRTmxoKw3XOluOCA/viewform) to get testnet $PROVE tokens. You will also need some Sepolia ETH. 

**For security, please create a fresh wallet specifically for this prover, as the private key will be used directly in the CLI**. We’ll transfer **1000 testnet PROVE** tokens to your wallet address on Sepolia along with some Sepolia ETH ****for gas. You’ll stake this PROVE to your prover to begin generating proofs.

## **3. Setup Your Prover**

Your prover requires stake in order to begin generating proofs; this stake provides economic security to your prover. To set up your prover, follow these steps:

- **Create a prover at** https://staking.sepolia.succinct.xyz/prover
- Stake **1,000 testnet $PROVE** to your **own prover** (not someone else’s) at https://staking.sepolia.succinct.xyz/prover

After creating your prover and staking to it, copy your **PROVER_ADDRESS**, which can be found under “My Prover” on the Prover tab. Also copy the **PRIVATE_KEY** of the fresh Sepolia address you created.

## **4. Install the Prover Node Software**

These commands download the prover node software. Run them in your terminal.

```bash
wget -O setup.sh https://gist.githubusercontent.com/0xCRASHOUT/6656b9418018c3657e612c34ae1546fd/raw/setup.sh
```

## **5. Run your Prover**

Before running your prover, make sure you’re in a `tmux` session to keep your prover running in the background (certain GPU setups come pre-installed with `tmux`  running; monitor your terminal to see whether you’re in one). 

```
sudo apt update && sudo apt install -y tmux

tmux new -s prover
```

To start your prover, run this command:

```bash
sudo bash setup.sh
```

**After the reboot, rerun** `sudo bash setup.sh`.

After successful setup, it will ask you to “Enter Prover Address”. Paste the **PROVER_ADDRESS** value you copied above. Next, it will ask you to “Enter Private Key”. Paste the **PRIVATE_KEY** value you got from above.

**Your prover will now start running and bidding for proofs in the network!** You can monitor your proofs in the Prover dashboard.

## **6. Share on X/Twitter**

Let the world know you're running a prover on the Succinct Network!

Post a photo or screenshot of your screen taken from your phone (bonus points if it shows your setup, location, or terminal running).

## **FAQs & Troubleshooting**

**How can I check if my proofs are successful?**

Your Prover dashboard shows the proofs you won and the testnet balance you’ve accrued.

**How can I change my node’s parameters?**

The script that generates proofs currently sets default parameters that we recommend. If you want to change these parameters, you can modify PROVE_PER_BPGU, the bid price, and PGUS_PER_SECOND, the maximum throughput of the prover, in script.sh.

**Common Errors**

- **Permanent error when Bid: request is not in the requested state**: This is normal. You lost a proof contest and the node will retry for another proof.
- **Permanent error when Bid: you do not have rights to bid**: You need to stake 1000 testnet $PROVE or you copied the incorrect PROVER_ADDRESS. Make sure you copied the address underneath “My Prover”.
- **Permanent error when Bid: you need to stake at least 1000 PROVE**: You need to stake 1,000 testnet $PROVE. Once staked, rerun sudo bash [setup.sh](http://setup.sh/).



