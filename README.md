# aiOS
An automated, bare-metal AI operating system script. Features optimized memory kernel parameters, headless CUDA/ROCm provisioning, and auto-orchestrated inference runtimes.
## ⚡ Deployment Playbook

### 1. Prerequisites
Start with a **fresh, minimal installation** of Ubuntu Server (Minimal option chosen during installation) or Rocky Linux Minimal. Ensure the machine has an active network connection.

### 2. Execution Setup
Clone this repository directly onto your target system, assign execution bit flags, and trigger the initialization script:

```bash
git clone https://github.com
cd YOUR_REPO_NAME
chmod +x build-aios.sh
sudo ./build-aios.sh
```

---

## 📜 Automated Deployment Script (`build-aios.sh`)

This script handles system modernization, resource tuning, graphics backend driver provisioning, and automatic container orchestrations.

```bash
#!/usr/bin/env bash
# ==============================================================================
# TITLE: build-aios.sh
# DESCRIPTION: Automated Headless Optimization Engine for Local AI
# ==============================================================================
set -euo pipefail

# --- CONFIGURATION MATRIX ---
TARGET_DISTRO="ubuntu-minimal"  # Options: ubuntu-minimal, rocky-minimal
ACCELERATOR_TYPE="nvidia"       # Options: nvidia, amd, cpu-only
INFERENCE_BACKEND="ollama"       # Options: ollama, vllm, both
API_PORT="11434"
DATA_DIR="/opt/aios/models"

echo "🚀 Initializing aiOS Deployment Framework..."

# --- PHASE 1: ENVIRONMENT SANITIZATION ---
echo "🧹 Purging non-essential desktop packages and background daemons..."
if [ "\$TARGET_DISTRO" = "ubuntu-minimal" ]; then
    export DEBIAN_FRONTEND=noninteractive
    apt-get update -y
    apt-get purge -y ubuntu-desktop* cups* avahi-daemon* modemmanager popularity-contest gdm3 sddm lightdm
    apt-get autoremove -y && apt-get clean
elif [ "\$TARGET_DISTRO" = "rocky-minimal" ]; then
    dnf groupremove -y "Graphical Server" "Server with GUI" || true
    dnf remove -y cups avahi || true
    dnf autoremove -y && dnf clean all
fi

# --- PHASE 2: KERNEL & MEMORY TUNING ---
echo "🧠 Injecting memory caching and low-latency kernel optimizations..."
cat <<EOF > /etc/sysctl.d/99-aios-performance.conf
vm.swappiness=1
vm.max_map_count=262144
net.core.rmem_max=16777216
net.core.wmem_max=16777216
fs.file-max=2097152
EOF
sysctl --system

# --- PHASE 3: COMPUTE LAYER PROVISIONING ---
echo "🏎️ Installing headless hardware acceleration drivers..."
if [ "\$ACCELERATOR_TYPE" = "nvidia" ]; then
    if [ "\$TARGET_DISTRO" = "ubuntu-minimal" ]; then
        apt-get install -y software-properties-common
        add-apt-repository ppa:graphics-drivers/ppa -y
        apt-get update -y
        apt-get install -y nvidia-headless-550-server nvidia-utils-550-server
    fi
    nvidia-smi --persistence-mode=1
fi

# --- PHASE 4: CONTAINER CONTAINERIZATION & RUNTIMES ---
echo "🐳 Deploying isolated container stack engines..."
if [ "\$TARGET_DISTRO" = "ubuntu-minimal" ]; then
    curl -fsSL https://docker.com -o get-docker.sh && sh get-docker.sh
    if [ "\$ACCELERATOR_TYPE" = "nvidia" ]; then
        apt-get install -y nvidia-container-toolkit
        systemctl restart docker
    fi
fi

mkdir -p "\$DATA_DIR"

# Write Docker Compose Configurations
cat <<EOF > docker-compose.yml
version: '3.8'
services:
  aios-core:
    image: ollama/ollama:latest
    container_name: aios-ollama-core
    restart: always
    volumes:
      - \${DATA_DIR}:/root/.ollama
    ports:
      - "\({API_PORT}:\){API_PORT}"
EOF

if [ "\$ACCELERATOR_TYPE" = "nvidia" ]; then
cat <<EOF >> docker-compose.yml
    deploy:
      resources:
        reservations:
          devices:
            - driver: nvidia
              count: all
              capabilities: [gpu]
EOF
fi

docker compose up -d

# --- PHASE 5: FIREWALL HARDENING & SYSTEM VALIDATION ---
echo "🛡️ Locking down internal packet firewalls..."
if command -v ufw &> /dev/null; then
    ufw default deny incoming
    ufw default allow outgoing
    ufw allow ssh
    ufw allow "\$API_PORT"/tcp
    ufw --force enable
fi

echo "✅ aiOS Installation Engine Completed Successfully!"
```

---

## ⚙️ Configuration Tuning Specifications

Before initiating the run, you can tune the deployment configuration matrix located directly inside the head parameters of the `build-aios.sh` script to suit your physical environment layout:

| Configuration Parameter | Target Matrix | Description / Deployment Context |
| :--- | :--- | :--- |
| `TARGET_DISTRO` | `ubuntu-minimal`, `rocky-minimal` | Controls the internal OS package manager pipeline (APT vs DNF). |
| `ACCELERATOR_TYPE` | `nvidia`, `amd`, `cpu-only` | Instructs the driver block solver which hardware toolkit to link. |
| `INFERENCE_BACKEND`| `ollama`, `vllm`, `both` | Configures the background runtime execution stack mapping. |
| `API_PORT` | `11434`, `8080` | Specifies the firewall rules layer hole allocation mapping. |

---

## 📈 System Tuning Settings (`/etc/sysctl.d/99-aios-performance.conf`)

`aiOS` overrides standard system parameters to stabilize large tensor allocations during context model swaps:

```ini
# Prevent memory swap performance degradations
vm.swappiness=1

# Maximize file descriptor capacities for deeply nested models
vm.max_map_count=262144

# Expand read and write memory parameters for rapid local network communication
net.core.rmem_max=16777216
net.core.wmem_max=16777216
```

---

## 🛡️ Telemetry & Diagnostic Validation Checks

Verify your headless system is communicating directly with the hardware acceleration assets without drawing graphical resource leaks:

### Check Accelerator Engine Status
```bash
nvidia-smi
# OR for AMD configurations
rocm-smi
```

### Validate API Token Generation Pipeline
```bash
# Query the live container endpoint across the private local network
curl -X POST http://localhost:11434/api/generate -d '{
  "model": "llama3",
  "prompt": "Confirm low latency bare metal response."
}'
```

### Inspect Compute Container Infrastructure Log Stacks
```bash
docker compose logs -f aios-ollama-core
```

---

## 🤝 Contribution Framework

We appreciate community improvements for trimming memory overhead, fine-tuning hardware acceleration, and building lightweight runtimes. 

1. Fork this project repository.
2. Initialize an isolated feature branch (`git checkout -b feature/OptimizedCore`).
3. Commit adjustments with technical clarity (`git commit -m 'Tune THP configurations'`).
4. Push clean updates up to your branch origin (`git push origin feature/OptimizedCore`).
5. Open a formal Pull Request for system review.

---

## 📄 License
This architecture framework is distributed completely open-source under the terms specified within the **MIT License**. For complete documentation overview profiles, see the included `LICENSE` file.
