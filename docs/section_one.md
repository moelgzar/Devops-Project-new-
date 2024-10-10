# **create VMs**

## 1 ubntu vm for K8S
## 1 ubntu vm for jenknis
## 1 ubntu vm for SonarQube
## 1 ubntu vm for Nexus 

## 1.1 - **install and setup K8S** 
 
 ### 1. Install Docker[On Master & Worker Node]
    write bash file in doxer.sh and excute it. 
     convert docer.sh to exeutable file 
    `sudo chmod +x docer.sh`
    ```bash
    sudo install -m 0755 -d /etc/apt/keyrings
    sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
    sudo chmod a+r /etc/apt/keyrings/docker.asc

    echo \
    "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://    download.docker.com/linux/ubuntu \
    $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
    sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
    sudo apt-get update

   
   
 
 ### 2. Install Required Dependencies for Kubernetes[On Master & Worker Node]
    ```bash
    sudo apt-get install -y apt-transport-https ca-certificates curl gnupg
    sudo mkdir -p -m 755 /etc/apt/keyrings
    ```
    
 ### 3. Add Kubernetes Repository and GPG Key[On Master & Worker Node]
 
    ```bash curl -fsSL https://pkgs.k8s.io/core:/stable:/v1.28/deb/Release.key | sudo gpg --dearmor -o /etc/apt/keyrings/kubernetes-apt-keyring.gpg
    echo 'deb [signed-by=/etc/apt/keyrings/kubernetes-apt-keyring.gpg] https://pkgs.k8s.io/core:/stable:/v1.28/deb/ /' | sudo tee /etc/apt/sources.list.d/kubernetes.list
    ```
 ### 4. Update Package List[On Master & Worker Node]
    `sudo apt update`
 
### 6. Install Kubernetes Components[On Master & Worker Node]
    `sudo apt install -y kubeadm=1.28.1-1.1 kubelet=1.28.1-1.1 kubectl=1.28.1-1.1`
 
### 7. Initialize Kubernetes Master Node [On MasterNode]
    `sudo kubeadm init --pod-network-cidr=10.244.0.0/16`
 
### 8. Configure Kubernetes Cluster [On MasterNode]
    ```bash
        mkdir -p $HOME/.kube
        sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
        sudo chown $(id -u):$(id -g) $HOME/.kube/config
```

 
## 1.2 Installing Jenkins on Ubuntu

```bash
#!/bin/bash

# Install OpenJDK 17 JRE Headless
sudo apt install openjdk-17-jre-headless -y

# Download Jenkins GPG key
sudo wget -O /usr/share/keyrings/jenkins-keyring.asc \
  https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key

#Add Jenkins repository to package manager sources
echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
  https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null

```
### Update package manager repositories

`sudo apt-get update`


### Install Jenkins
sudo apt-get install jenkins -y

### *Save this script in a file, for example, install_jenkins.sh, and make it executable using:*
       `chmod +x install_docker.sh`
       `./install_docker.sh`


## install docer for furture use :
```bash
#!/bin/bash

#Update package manager repositories
sudo apt-get update

#Install necessary dependencies
sudo apt-get install -y ca-certificates curl

#Create directory for Docker GPG key
sudo install -m 0755 -d /etc/apt/keyrings

#Download Docker's GPG key
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc

#Ensure proper permissions for the key
sudo chmod a+r /etc/apt/keyrings/docker.asc

#Add Docker repository to Apt sources
echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
$(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

#Update package manager repositories
sudo apt-get update

#Install Docker components
sudo apt-get install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

### Save this script in a file, for example, install_docker.sh, and make it executable using
   
    `chmod +x install_docker.sh`

### Then, you can run the script using:
    `./install_docker.sh`



