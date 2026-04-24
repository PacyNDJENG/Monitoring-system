# Monitoring System
🖥️ Distributed Monitoring Infrastructure

📌 Overview
This project implements a secure distributed monitoring system designed to supervise multiple machines (Linux & Windows) through a centralized dashboard.
It is based on a manager–agent architecture, secured via a private VPN network and fully containerized using Docker.

🎯 Objectives
Centralize system monitoring across multiple machines
Enable secure communication between isolated networks
Deploy a scalable containerized infrastructure
Implement real-time performance monitoring
Solve real-world networking and system integration challenges

🏗️ Architecture
[ Windows Agent ]     [ Linux Agent ]
        \                 /
         \               /
        🔐 Tailscale VPN Network
                 |
                 ↓
     🖥️ Beszel Monitoring Server
        (Docker - Port 8090)
                 |
                 ↓
          📊 Web Dashboard

⚙️ Technologies Used
  🐳 Docker & Docker Compose
  📡 Beszel (Monitoring System)
  🔐 Tailscale
  🐧 Linux (Ubuntu Server)
  🪟 Windows Agents
  🧰 Bash & PowerShell   
  
🚀 Deployment
1. Clone repository
  ```bash git clone https://github.com/pacyNDJENG/Monitoring-system.git
  cd Monitoring-system
```
2. Start server
   ```bash
   docker compose up -d
   ```
   
📍 Access dashboard:
   http://localhost:8090

🖥️ Agents Setup
🐧 Linux Agent
  ```bash 
  scripts/install-agent-ubuntu.sh
```
🪟 Windows Agent
 ```bash 
 .\scripts\install-agent-windows.ps1
```

🔐 Network Layer (Tailscale)
Secure communication is handled via VPN mesh network: 
  ```bash curl -fsSL https://tailscale.com/install.sh | sh
     sudo tailscale up
  ```
  ✔ Private IPs (100.x.x.x)
  ✔ Encrypted communication
  ✔ Cross-network connectivity
  
🔧 Infrastructure Services Layer (Apache & Postfix)
In addition to system metrics monitoring, this infrastructure also supervises critical server services:

🌐 **Apache Web Server**
📧 **Postfix Mail Server**
These services are installed and managed on monitored nodes and their availability is part of the infrastructure health tracking.

## 🌐 Apache Web Server Monitoring
Apache is used as a web service to validate server availability.

## 🌐 Apache Installation
```bash
sudo apt update
sudo apt install apache2 -y
```

### Service management
```bash
id="apache2"
sudo systemctl start apache2
sudo systemctl enable apache2
sudo systemctl status apache2
```

### Test service
```bash bash id="apache3"
curl http://localhost
```
✔ Used to verify HTTP service availability

## 📧 Postfix Mail Server Monitoring
Postfix is used as a mail transfer agent for testing email delivery services.

### Installation
```bash
id="postfix1"
sudo apt update
sudo apt install postfix -y
```

### Service management
```bash
id="postfix2"
sudo systemctl start postfix
sudo systemctl enable postfix
sudo systemctl status postfix
```

### Test mail delivery
```bash
id="postfix3"
echo "Test email from monitoring system" | mail -s "Postfix Test" user@example.com
```
✔ Used to verify SMTP service availability


## 📊 Integration into Monitoring System
Both services are monitored as part of the infrastructure health layer:

* Service status (running / stopped)
* Availability checks
* System-level health correlation
This extends monitoring beyond system metrics into **service-level observability**.

⚠️ Challenges & Solutions
❌ Docker permission issues
✔ Fixed using user group configuration:
    sudo usermod -aG docker $USER
❌ Network isolation between machines
✔ Solved using Tailscale VPN mesh network
❌ Agents offline
✔ Fixed by unifying network layer and server address

📊 Results
✔ Fully functional distributed monitoring system
✔ Secure multi-machine communication
✔ Real-time metrics dashboard
✔ Stable containerized deployment
✔ Production-like architecture simulation

🧠 Key Learning Outcomes
Distributed system architecture design
Containerized infrastructure deployment
VPN-based secure networking
Linux system administration
Debugging real-world infrastructure issues

🚀 Future Improvements
Integration with Prometheus
Visualization using Grafana
Alerting system (email/webhooks)
Kubernetes deployment
Centralized logging (ELK stack)

📜 License
Educational / Portfolio Project

🏁 Conclusion
This project demonstrates a real-world distributed monitoring infrastructure, combining:
containerization
secure networking
system administration
and multi-agent architecture
It reflects practical DevOps and infrastructure engineering skills suitable for professional environments.
