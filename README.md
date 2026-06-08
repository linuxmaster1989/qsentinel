# Q-Sentinel: Hybrid Quantum-Classical Threat Intelligence (v2.0.0)

Q-Sentinel is a hybrid quantum-classical security auditor and network intelligence engine that leverages Simon's Algorithm on the physical, cloud-hosted **Rigetti Cepheus-1 108-Qubit QPU** and **AWS SV1 Simulators**. It ingests and parses local server logs to capture advanced brute-force periodicities, botnet cadences, and web scrapers masking their footprints across your endpoints.

Verified functional on Ubuntu 24.04 LTS via remote terminal staging tests — June 2026.

---

## 🔒 The Zero-Privilege Security Model
Unlike legacy endpoint monitoring utilities that demand root access to scrape system logs, Q-Sentinel v2.0.0 completely decouples execution paths from `sudo` prerequisites. 

**Why this is critical:** Running complex quantum abstraction SDKs under a root shell completely strips or breaks local environment paths, custom Python site-packages, and user-specific AWS IAM credentials tokens. Q-Sentinel safely isolates its analytical layer by operating strictly on unprivileged log dumps staged manually within the application runtime directory. Your AWS credentials and system binaries remain completely secure.

---

## 🛠️ Installation & Environment Setup

### 1. Update Platform Packages & AWS CLI Configuration
Install standard terminal utilities required to unpack archives and establish secure upstream web sockets with AWS Braket endpoints:

```bash
sudo apt update && sudo apt upgrade -y
sudo apt install python3-pip unzip curl tar -y

# Download and deploy the AWS CLI Layer
curl "[https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip](https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip)" -o "awscliv2.zip"
unzip awscliv2.zip
sudo ./aws/install
rm -rf awscliv2.zip aws/
aws configure
# AWS Access Key ID: [Your-IAM-Access-Key]
# AWS Secret Access Key: [Your-IAM-Secret-Key]
# Default region name: us-west-1
# Default output format: json
# Pull essential interactive terminal menus and the Amazon Braket Python environment
pip3 install amazon-braket-sdk questionary boto3

# Extract the production software archive
tar -xvf q-sentinel-v2.0-rigetti.tar.gz
cd q-sentinel-v2.0-rigetti
# For SSH Authentication Audit:
sudo cp /var/log/auth.log ./auth.log
sudo chown $USER:$USER ./auth.log
sudo chmod 644 ./auth.log

# For aaPanel/Nginx Web Server Access Audit:
# (Adjust path if your custom log directory varies)
sudo cp /www/wwwlogs/access.log ./access.log
sudo chown $USER:$USER ./access.log
sudo chmod 644 ./access.log
python3 main.py
q-sentinel-v2.0-rigetti/
├── main.py                # Primary CLI matrix, ledger tracking engine, and interactive hub
├── log_parser.py          # Log ingestion regex patterns and zero-privilege DNS/WHOIS mappers
├── quantum_processor.py   # Simon's algorithm circuit composition and AWS Braket S3 automation
├── .gitignore             # Critical block list ensuring logs/databases are never committed to git
├── auth.log               # [Staged Source] Localized unprivileged SSH log trace
└── access.log             # [Staged Source] Localized unprivileged aaPanel/Web server access log
====================================================
   Q-SENTINEL: COST-EFFICIENT QPU AUDIT (v2.0.0)
====================================================
REQUIREMENT: AWS CLI MUST BE SET TO 'us-west-1'
? Select Action: 
  0. QPU Telemetry
  1. SV1 Simulator
  2. Cepheus-1 QPU
❯ 3. Threat Intelligence Hub
  Exit
sudo ufw deny from <Malicious-IP> to any
