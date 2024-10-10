
# Create Sonarqube Docker container

### To run SonarQube in a Docker container with the provided command, you can follow these steps:
### 1.  log in to your Docker Hub account from your Docker host, you can use the following command: 

`docker login`

### 2. Open your terminal.
### Enter your Docker Hub username when prompted:
`Username: your_dockerhub_username`
### 3. Enter your Docker Hub password:
`Password: your_dockerhub_password`
### it will print Login Succeeded

### 2. Run the following command:

`docker run -d --name sonar --network host sonarqube:lts-community`
    
**Note: i use -- network host to can abel to access my image from host machine**

### This command will download the sonarqube:lts-community Docker image from Docker Hub if it's not already available locally. Then, it will create a container named "sonar" from this image, running it in detached mode (-d flag) and mapping port 9000 on the host machine to port 9000 in the container (<ip-addrees-for-this-machine:9000> ).

# Install and SetUp Nexus 
    ```bash 
    #!/bin/bash

    # Update package manager repositories
    sudo apt-get update

    # Install necessary dependencies
    sudo apt-get install -y ca-certificates curl

    # Create directory for Docker GPG key
    sudo install -m 0755 -d /etc/apt/keyrings

    # Download Docker's GPG key
    sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc

    # Ensure proper permissions for the key
    sudo chmod a+r /etc/apt/keyrings/docker.asc

    # Add Docker repository to Apt sources
    echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
    $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
    sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

    # Update package manager repositories
    sudo apt-get update

    sudo apt-get install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
    ```

### Save this script in a file, for example, install_docker.sh, and make it executable using:

`chmod +x install_docker.sh`
### Then, you can run the script using:

`./install_docker.sh`

## Create Nexus container


### To create a Docker containe 3 and exposing it on port 8081, you can use the following command: 
`docker run -d --name nexus -network host  sonatype/nexus3:latest` 
### After running this command, Nexus will be accessible on your host machine at http://IP:8081.

## Get Nexus default password
#### Your provided commands are correct for accessing the Nexus password stored in the container. Here's a breakdown of the steps:

### Get Container ID
`docker ps`

### Access Container's Bash Shell: Once you have the container ID, you can execute the docker exec command to access the container's bash shell:
`docker exec -it <container_ID> /bin/bash`
### Navigate to Nexus Directory:
`cd sonatype-work/nexus3`
### View Admin Password: Finally, you can view the admin password by displaying the contents of the admin.password file:

`cat admin.password`

### Exit the Container Shell:
`exit`
### This process allows you to access the Nexus admin password stored within the container. Make sure to keep this password secure, as it grants administrative access to your Nexus instance.

