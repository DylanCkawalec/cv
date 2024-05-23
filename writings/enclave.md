# Secure Server Setup for Rust-SGX Development with Docker (Fortanix EDP)

## Introduction

This guide will walk you through configuring an Ubuntu 22.04 LTS server for secure application development using Rust-SGX (Fortanix EDP), Docker containers, and additional security-enhancing tools like Trust-DNS, Rustls, and Certbot. The purpose of this guide is to get our Decentralized Front End Demonstration Server for secure application development ready to be used to deploy the Osmosis Front End, as we believe this is

![DFE Org](https://github.com/DylanCkawalec/cv/assets/43707795/69e83ded-c73c-4702-9261-a70cef206e93)

## Prerequisites

* **Operating System:** Ubuntu 22.04 LTS (ensure it's fully updated)
* **SGX-Compatible Hardware:** A server with Intel SGX enabled in BIOS and supported by the Linux kernel
* **User Credentials:**  Replace placeholders (`dylankawalec`, `dfekey`, `00.00.000.000`) with your actual credentials
* **SSH Key Pair:** A strong SSH key pair (e.g., generated with `ssh-keygen`)

## 1. Secure SSH Access

1. **Place SSH Key:** 
   ```bash
   mv ~/Desktop/dfekey.pem ~/.ssh/
   chmod 600 ~/.ssh/dfekey.pem
   ```

2. **SSH Agent:**
   ```bash
   eval "$(ssh-agent -s)"
   ssh-add ~/.ssh/dfekey.pem
   ```

3. **SSH Config (`~/.ssh/config`):**
   ```
   Host your_server_alias
     Hostname 00.00.000.000
     User dylankawalec
     IdentityFile ~/.ssh/dfekey.pem
   ```

4. **User Password (Optional, but recommended):**
   ```bash
   sudo passwd dylankawalec
   ```

## 2. Connect to Server

* **SSH:** `ssh your_server_alias`
* **VS Code:** Use the "Remote - SSH" extension

## 3. Verify SGX Support

```bash
lscpu | grep sgx
dmesg | grep sgx
```

If both commands show output related to SGX, your hardware is ready.

## 4. Prepare System Environment

```bash
sudo apt update && sudo apt upgrade -y

sudo apt install build-essential git curl wget \
                 linux-headers-$(uname -r) dkms \
                 autoconf automake libtool \
                 protobuf-compiler libboost-all-dev \
                 libssl-dev libcurl4-openssl-dev libprotobuf-dev debhelper cmake reprepro unzip pkgconf \
                 libboost-system-dev libboost-thread-dev lsb-release libsystemd-dev \
                 ocaml ocamlbuild \
                 libcurl4 libprotobuf-dev libssl-dev \
                 python3 python3-pip \
                 g++ gcc make cmake pkg-config -y 
```

## 5. Install Rust & Fortanix SGX Toolkit

```bash
curl --proto '=https' --tlsv1.2 -sSf [https://sh.rustup.rs](https://sh.rustup.rs) | sh
source "$HOME/.cargo/env"
rustup upgrade
rustup toolchain install nightly
rustup update nightly
rustup target add x86_64-fortanix-unknown-sgx --toolchain nightly
cargo install fortanix-sgx-tools sgx-tools
echo -e '[target.x86_64-fortanix-unknown-sgx]\nrunner="ftxsgx-runner-cargo"' >> ~/.cargo/config
```

## 6. Install Node.js, Docker, and Security Tools

```bash
curl -fsSL [https://deb.nodesource.com/setup_lts.x](https://deb.nodesource.com/setup_lts.x) | sudo -E bash -
sudo apt-get install -y nodejs

# Docker (follow official instructions for the latest version)
curl -fsSL [https://get.docker.com](https://get.docker.com) -o get-docker.sh
sudo sh get-docker.sh

sudo usermod -aG docker $USER

cargo install trust-dns rustls 
sudo apt-get install -y certbot
curl [https://bun.sh/install](https://bun.sh/install) | bash
```

## 7. Re-verify SGX

```bash
sgx-detect --verbose
```


## Additional Notes

**User Permissions:**
- **Ensure your user is part of the `docker` group**: This allows you to run Docker commands without using `sudo`.
    ```bash
    sudo usermod -aG docker $USER
    newgrp docker
    ```

**Firewall:**
- **Configure your firewall**: Allow traffic on the ports your applications will use. This step is crucial for both development and production environments to ensure that your applications are accessible and secure.
    ```bash
    sudo ufw allow <your-port-number>
    sudo ufw enable
    ```

**Environment Variables:**
- **Set `SGX_SDK` and `SGX_MODE`**: These environment variables are necessary for the SGX SDK to function correctly.
    ```bash
    export SGX_SDK=/path/to/sgxsdk
    export SGX_MODE=HW  # or SIM for simulation mode
    ```

### Expanded Steps

**1. User Permissions:**
Adding your user to the `docker` group removes the need to prefix Docker commands with `sudo`.

**2. Firewall Configuration:**
Proper firewall configuration ensures that only necessary ports are open, minimizing security risks.

**3. Setting Environment Variables:**
Environment variables ensure that the SGX SDK and runtime can locate necessary files and operate in the correct mode.

### Verification Steps

**1. Verify User Permissions:**
   ```bash
   docker run hello-world
   ```
   - **Purpose**: Confirms you can run Docker commands without `sudo`.
   - **Expected Output**: A message from the "hello-world" Docker container.

**2. Verify Firewall Rules:**
   ```bash
   sudo ufw status
   ```
   - **Purpose**: Ensures that the required ports are open.
   - **Expected Output**: List of allowed ports.

**3. Verify Environment Variables:**
   ```bash
   echo $SGX_SDK
   echo $SGX_MODE
   ```
   - **Purpose**: Confirms that environment variables are set correctly.
   - **Expected Output**: Paths and mode for SGX SDK.


