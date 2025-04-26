# docker_images

# 🚀 Docker Setup & Image Management on Ubuntu 20.04 LTS  
By **Oyebola**  

This guide walks through Docker installation, setting up repositories, working with images, writing a Dockerfile, and managing containers efficiently.

---

## 🛠 Docker Installation  

Start by updating your package list and installing essential dependencies:

```bash
sudo apt-get update  
sudo apt-get install ca-certificates curl gnupg

🔑 Adding Docker GPG Key
Create the directory for storing keyrings and download the Docker GPG key:
sudo install -m 0755 -d /etc/apt/keyrings  
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg  
sudo chmod a+r /etc/apt/keyrings/docker.gpg

🏗 Adding Docker Repository
Configure the APT repository to retrieve Docker packages:
echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] \
https://download.docker.com/linux/ubuntu $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
sudo tee /etc/apt/sources.list.d/docker.list > /dev/null  


Then, refresh package lists:
sudo apt-get update  


📦 Installing Docker
Install Docker and its essential plugins:
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin  



✅ Verifying Installation
Run the "Hello World" container to ensure Docker is correctly installed:
sudo docker run hello-world  


Expected Output:
- Docker pulls the hello-world image.
- Runs a container that prints a greeting message.
- Confirms that installation is successful!

👤 Managing Docker Permissions
Allow the logged-in user (azureuser) to execute Docker commands without sudo:
sudo usermod -aG docker azureuser  
newgrp docker  


If permissions issues occur, fix them using:
sudo chown $USER /var/run/docker.sock  



🖼 Exploring Docker Images
Search for available images on Docker Hub:
docker search ubuntu  


List downloaded images:
docker images  


List running containers:
docker ps  


List all (including stopped) containers:
docker ps -a  


Stop a container:
docker stop <container_ID>  


Remove an image from the system:
docker rmi <image_ID>  



📝 Writing a Dockerfile
Let's create an NGINX container using a custom Dockerfile:
# Use the official NGINX base image  
FROM nginx:latest  

# Set the working directory in the container  
WORKDIR /usr/share/nginx/html/  

# Copy the local HTML file to NGINX default public directory  
COPY index.html /usr/share/nginx/html/  

# Expose port 80 to allow external access  
EXPOSE 80  

# No CMD needed—NGINX image comes with a default server startup  


Create an index.html file:
echo "Welcome to Darey.io" >> index.html  



🔨 Building & Running the Custom NGINX Image
Build the Docker image:
docker build -t dockerfile .  


(The . at the end is very important—it signifies the current directory as the build context.)
Run a container based on the custom image:
docker run -p 8080:80 dockerfile  



🏷 Tagging & Pushing Docker Images
Tag your Docker image:
docker tag dockerfile boaxyl/my_nginx:1.0  


Login to Docker Hub:
docker login -u boaxyl
Entered the password on the CLI to authenticate successfully

Push the image to Docker Hub:
docker push boaxyl/my_nginx:1.0  



🎯 Summary
- Installed Docker on Ubuntu.
- Created a custom NGINX container using a Dockerfile.
- Built and ran the container.
- Pushed the image to Docker Hub.
