# 03 — Docker & Kubernetes

## What you learn here
- How apps were deployed traditionally (directly on OS)
- What is a Hypervisor / VM (VirtualBox, AWS EC2)
- What is Docker and how it differs from VMs
- What is Kubernetes and why it's needed

## Run order
```bash
python 01_traditional.py          # no isolation — runs directly on OS
python 02_hypervisor_simulated.py # VM simulation with logs
python 03_hypervisor_real_code.py # real VM creation (VirtualBox + AWS)
python 04_docker.py               # containers
python 05_kubernetes.py           # orchestration
```

## Key concepts

### Evolution of app deployment
```
2000s: Traditional → app runs directly on OS (breaks on other machines)
2005s: Hypervisor  → VMs isolate apps (heavy, slow)
2013:  Docker      → containers isolate apps (lightweight, fast)
2014:  Kubernetes  → manages many containers automatically
```

### VM vs Docker
| | VM | Docker |
|--|--|--|
| Startup | 2-3 min | 2-3 sec |
| RAM | 1-2 GB | 50-200 MB |
| Isolation | Full OS | Process-level |
| Runs different OS | ✅ | ❌ |

### Hypervisor types
```
Type 1 (Bare Metal):   Hardware → Hypervisor → VMs   (used in AWS, Azure)
Type 2 (Hosted):       Hardware → OS → VirtualBox → VMs   (used locally)
```

### Real VM creation (03_hypervisor_real_code.py)
- **VirtualBox** → uses `VBoxManage` CLI commands via `subprocess`
- **AWS EC2** → uses `boto3` Python SDK to call AWS API
- Dummy AWS keys used in code — replace with real keys to actually create VMs

## Prerequisites for real VM creation

### VirtualBox (local)
```bash
brew install --cask virtualbox
```

### AWS EC2 (cloud)
```bash
pip install boto3
# Get real keys from: AWS Console → IAM → Access Keys
```
