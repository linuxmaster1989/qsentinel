MUST USE SUDO

"Verified functional on Ubuntu 24.04 via GitHub clone test - May 2026."

sudo apt update && sudo apt upgrade -y
sudo apt install python3-pip unzip curl -y

curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
unzip awscliv2.zip
sudo ./aws/install
rm -rf awscliv2.zip aws/

sudo aws configure
# Set Region to: us-west-1

sudo pip3 install amazon-braket-sdk questionary

tar -xvf q-sentinel-v1.8-rigetti.tar.gz
cd q-sentinel-v1.8-rigetti

sudo python3 main.py
