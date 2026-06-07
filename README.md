# Q-Sentinel: Cost-Efficient QPU Audit (v1.8.1)

Q-Sentinel is a hybrid quantum-classical security auditor that leverages **Simon's Algorithm** on the cloud-hosted **Rigetti Cepheus-1 108-Qubit QPU** and **AWS SV1 Simulators**. It ingests and parses local server logs to identify advanced brute-force patterns, credential-stuffing anomalies, and botnet connection periodicity.

> **Verified functional on Ubuntu 24.04 via GitHub clone test - June 2026.**

---

## 🔒 The Zero-Privilege Security Model

Unlike older security tools that require root access to read system logs, **Q-Sentinel v1.8.1 completely removes the requirement for `sudo` execution.** Running quantum tools under `sudo` strips out or breaks user-specific environment configurations, such as your AWS terminal profile tokens and local Python paths. Q-Sentinel is hardcoded to parse unprivileged log copies placed directly in the program's working directory, keeping your active IAM credentials active and safe.

---

## 🛠️ Installation & Environment Setup

### 1. Update Core Packages
Install standard system utilities required for unpacking and managing the tool:
```bash
sudo apt update && sudo apt upgrade -y
sudo apt install python3-pip unzip curl tar -y
curl "[https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip](https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip)" -o "awscliv2.zip"
unzip awscliv2.zip
sudo ./aws/install
rm -rf awscliv2.zip aws/
aws configure
AWS Access Key ID: Your_Access_Key
AWS Secret Access Key: Your_Secret_Key
Default region name: us-west-1
Default output format: json
pip3 install amazon-braket-sdk questionary boto3
tar -xvf q-sentinel-v1.8-rigetti.tar.gz
cd q-sentinel-v1.8-rigetti
# Copy the live auth log to the root directory of the program
sudo cp /var/log/auth.log ./auth.log

# Change ownership to your standard terminal user
sudo chown $USER:$USER ./auth.log
sudo chmod 644 ./auth.log
python3 main.py
q-sentinel-v1.8-rigetti/
├── main.py                # Core menu engine and data tracking manager
├── log_parser.py          # Log ingestion and regex filtering hooks
├── quantum_processor.py   # Simon's circuit logic and AWS S3 automation hooks
├── .gitignore             # Block logs and json databases from being pushed
└── auth.log               # <--- Your staged local log copy goes here
