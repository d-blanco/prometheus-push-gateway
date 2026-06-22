# Deploy the Monitoring Environment

This stack provides:  
•	Grafana dashboards  
•	Prometheus metrics collection  
•	Pushgateway for CI/CD metrics ingestion  

These instructions are intended for amazonlinux2023 on AWS ec2 instance.


## Required Security Group Rules
Allow inbound access to the following ports:  
Port	Purpose
22	SSH
3000 |	Grafana  
9090 |	Prometheus  
9091 |	Pushgateway  

For lab purposes:    
22  |   0.0.0.0/0  
3000 |  0.0.0.0/0  
9090 |  0.0.0.0/0  
9091 |  0.0.0.0/0  

## Install Docker
Amazon Linux Example:
```
sudo dnf install -y docker

sudo systemctl enable docker
sudo systemctl start docker

sudo usermod -aG docker $USER

newgrp docker

docker ps
```
## Install Docker Compose
Download Docker Compose:
```
wget https://github.com/docker/compose/releases/download/v2.39.1/docker-compose-linux-x86_64
# Make executable:
chmod +x docker-compose-linux-x86_64
# Move into path:
sudo mv docker-compose-linux-x86_64 /usr/local/bin/docker-compose
# Verify:
docker-compose version
```

##  Deploy Monitoring Stack
Clone the repository:
```
git clone https://github.com/d-blanco/prometheus-push-gateway.git

cd prometheus-push-gateway
Start the stack:
docker-compose up -d
```
Verify containers:  
docker ps  
Access:  
Grafana:    http://<PUBLIC_IP>:3000  
Prometheus: http://<PUBLIC_IP>:9090  
