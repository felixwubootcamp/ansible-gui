## **Ansible Semaphore Setup Guide**

### **Prerequisites**:
- An Ubuntu server.

---

### **1. Installing Docker**:

1. **Update Package Information**:
   ```bash
   sudo apt update
   ```

2. **Install Required Packages**:
   ```bash
   sudo apt install apt-transport-https ca-certificates curl software-properties-common -y
   ```

3. **Add Docker's Official GPG Key**:
   ```bash
   curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
   ```

4. **Add Docker Repository**:
   ```bash
   sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
   ```

5. **Install Docker**:
   ```bash
   sudo apt update
   sudo apt install docker-ce -y
   ```

6. **Start and Enable Docker**:
   ```bash
   sudo systemctl start docker
   sudo systemctl enable docker
   ```

---

### **2. Installing Docker Compose**:

1. **Download Docker Compose**:
   ```bash
   sudo curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
   ```

2. **Make Docker Compose Executable**:
   ```bash
   sudo chmod +x /usr/local/bin/docker-compose
   ```

---

### **3. Installing Essential Dependencies**:

1. **Install Git**:
   ```bash
   sudo apt install git -y
   ```

---

### **4. Downloading and Installing Semaphore**:

1. **Navigate to Temporary Directory**:
   ```bash
   cd /tmp
   ```

2. **Download Semaphore**:
   ```bash
   wget https://github.com/ansible-semaphore/semaphore/releases/download/v2.8.75/semaphore_2.8.75_linux_amd64.deb
   ```

3. **Install Semaphore**:
   ```bash
   sudo dpkg -i semaphore_2.8.75_linux_amd64.deb
   ```

---

### **5. Docker Compose Configuration for Semaphore**:

1. **Create Configuration Directory**:
   ```bash
   mkdir ~/semaphore_docker
   cd ~/semaphore_docker
   ```

2. **Create Configuration Files**:
   ```bash
   touch docker-compose.yml .env
   ```

---

### **6. Setting Up Environment Variables**:

1. **Define Variables in `.env` File**:
   - MYSQL_PASSWORD: MySQL password
   - SEMAPHORE_DB_PASS: Semaphore database password
   - SEMAPHORE_ADMIN_PASSWORD: Admin password for Semaphore
   - SEMAPHORE_ACCESS_KEY_ENCRYPTION: Encryption key for access keys

2. **Generate Encryption Key**:
   ```bash
   echo "SEMAPHORE_ACCESS_KEY_ENCRYPTION=$(head -c32 /dev/urandom | base64)" >> .env
   ```

---

### **7. Docker Compose Configuration**:

- Add the provided Docker Compose configuration to the `docker-compose.yml` file.

---

### **8. Security Recommendations**:

- Regularly update Docker images.
- Implement firewall rules to restrict access.
- Use monitoring tools like `fail2ban`.
- Regularly backup critical data.
- Monitor system and Docker logs.

---

### **9. Deploying Semaphore**:

1. **Start Services**:
   ```bash
   docker-compose up -d
   ```

2. **Access Semaphore**:
   - Open a web browser and navigate to [http://localhost:3000](http://localhost:3000/).

---

**Note**: Ensure to replace placeholders with actual values and keep confidential information secure.

---

I hope this structured guide will be helpful for your client. If you need any further adjustments or have questions, please let me know!
