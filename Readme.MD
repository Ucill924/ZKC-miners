# Boundless Miner Guide

This guide provides step-by-step instructions for setting up and running a Boundless miner on a VPS with a single NVIDIA GPU on Ubuntu 24.04. It covers prerequisites, installation, configuration, staking, enabling the prover, mining, and claiming rewards using the Sepolia testnet.



## Prerequisites

### Operating System
- **OS**: Ubuntu 24.04 (required)

### Hardware
- **GPU**: High-performance NVIDIA GPU (e.g., RTX 3090, 4090, A6000)
- **Clock Speed**: ≥ 3.0GHz boost
- **RAM**: 32 GB DDR4 (minimum)
- **Storage**: 200 GB SSD (NVMe preferred)

### CLI Tools
- `git`
- `cargo`
- `docker`
- `docker-compose`
- `just`
- `nvidia-container-toolkit`

## Install Prerequisites

Update the system and install required packages:

```bash
sudo apt update && sudo apt upgrade -y
sudo apt install -y \
    build-essential \
    curl \
    wget \
    git \
    unzip \
    zip \
    software-properties-common \
    ca-certificates \
    gnupg \
    lsb-release \
    htop \
    net-tools \
    neofetch \
    tmux \
    vim
sudo apt install -y pkg-config libssl-dev
sudo apt-get update -qq && sudo apt-get install -y -q clang
```


## Clone the Boundless repository and switch to the release-1.0 branch:
```bash
git clone https://github.com/boundless-xyz/boundless
cd boundless
git checkout release-1.0
```

## Install Dependencies

```bash
sudo ./scripts/setup.sh
```

## Install RustInstall Rust and add it to your PATH:


curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
source $HOME/.cargo/env
```


## Install RISC Zero
```bash
curl -L https://risczero.com/install | bash
source "/root/.bashrc"
```

Verify the installation:

```bash
rzup --version
```


## Run rzup to install the necessary components (rust, cargo-risc-zero, cpp, r0vm):
```bash
rzup install
```




## Install Bento

```bash
cargo install --git https://github.com/risc0/risc0 bento-client --bin bento_cli
```


Add bento to your PATH:
```bash
cargo install --locked --git https://github.com/boundless-xyz/boundless boundless-cli --branch release-1.0 --bin boundless
export PATH="$HOME/.cargo/bin:$PATH"
echo 'export PATH="$HOME/.cargo/bin:$PATH"' >> ~/.bashrc
source ~/.bashrc
```

## Install Boundless CLI

```bash
cargo install --locked --git https://github.com/boundless-xyz/boundless boundless-cli --branch release-1.0 --bin boundless
```


## Install risc0-groth16 using rzup
```bash
rzup install risc0-groth16
```



## Specify the Reward Address

Before starting Bento again, provers need to enable the ZK mining feature. This requires a valid Ethereum address set to the REWARD_ADDRESS environment variable. 
It is recommended to set this directly in the compose.yml file:

```bash
x-base-environment: &base-environment
DATABASE_URL: postgresql://${POSTGRES_USER:-worker}:${POSTGRES_PASSWORD:-password}@${POSTGRES_HOST:-postgres}:${POSTGRES_PORT:-5432}/${POSTGRES_DB:-taskdb}
REDIS_URL: redis://${REDIS_HOST:-redis}:6379
S3_URL: http://${MINIO_HOST:-minio}:9000
S3_BUCKET: ${MINIO_BUCKET:-workflow}
S3_ACCESS_KEY: ${MINIO_ROOT_USER:-admin}
S3_SECRET_KEY: ${MINIO_ROOT_PASS:-password}
RUST_LOG: ${RUST_LOG:-info}
RISC0_HOME: /usr/local/risc0
RUST_BACKTRACE: 1
REWARD_ADDRESS: "0x1234...5678"
The remain txt
```

## Create env.rpc
Edit file .env.rpc with your priavtkey for provers and RPC

```bash 
export PRIVATE_KEY=0x_your_privatekey
export RPC_URL=https://base-mainnet.g.alchemy.com/v2/Yourkey_alchemi
```

## Runing Bento And Broker

```bash
Source .env.rpc
```

## Runing Bento
```bash
Just Bento
```

## Runing Broker

```bash
Just broker 
```

## Check Log
```bash
Just broker logs
```


## Stop Prover
```bash
Just broker down
```

## For more information on how to submit work logs and claim rewards, visit  https://docs.boundless.network/















