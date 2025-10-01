# Boundless Miner Guide (Single GPU)

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
