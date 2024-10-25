# Overview
This project involves deploying the Node.js application from the Node.js GitHub repository 
to a local Kubernetes cluster. The deployment will use ArgoCD for continuous delivery. We 
will set up a Jenkins pipeline to automate the build and deployment process.
# Prerequisites
• Virtual Machine (VM) for Jenkins
• Docker installed on the Jenkins VM
• Another VM for Minikube and kubectl
• Minikube installed on the second VM
• ArgoCD installed on Minikube
• Jenkins installed on the first VM
• GitHub account
• Docker Hub account
# machine for jenkins and Docker 

# install Docker
```bash
sudo apt update
sudo apt install curl
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/trusted.gpg.d/docker.gpg
sudo add-apt-repository "deb [arch=$(dpkg --print-architecture)] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
sudo apt update
sudo apt -y install lsb-release gnupg apt-transport-https ca-certificates curl software-properties-common
sudo apt -y install docker-ce docker-ce-cli containerd.io docker-compose-plugin docker-registry
sudo usermod -aG docker $USER
newgrp docker
```
# Install Jenkins on local host
```bash

sudo wget -O /usr/share/keyrings/jenkins-keyring.asc https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key

echo "deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc]" https://pkg.jenkins.io/debian-stable binary/ | sudo tee /etc/apt/sources.list.d/jenkins.list > /dev/null

sudo apt update
sudo apt install fontconfig openjdk-17-jre -y
sudo apt install -y jenkins
sudo systemctl start jenkins
sudo systemctl status jenkins

Jenkins URL ====>>  http://Your-Machine-IP:8080
```
After writing the Docker File and Jenkins File, enter the Jenkins GUI, create a jop pipline, and run Buildnow.

![image](https://github.com/user-attachments/assets/a0cad970-d2e0-4f12-972c-e0f1d26bb446)

![image](https://github.com/user-attachments/assets/15aa3211-3a24-42ac-9b9d-a82dcef5df8a)


![image](https://github.com/user-attachments/assets/0937d2d8-16fb-4a8b-b837-b3ffdb453e20)

![image](https://github.com/user-attachments/assets/5eae3d62-817d-44c7-9ded-a267e0ce5afb)

![image](https://github.com/user-attachments/assets/082f9cac-b6e2-47e6-97d7-8fbc04bcd7ad)

![image](https://github.com/user-attachments/assets/31daf16a-32b1-4931-8e09-9ce3de9745c9)

![image](https://github.com/user-attachments/assets/f6da31f4-bf85-40cb-8af3-0bd99acc6c3c)

# ensure now DockerHub
![image](https://github.com/user-attachments/assets/aa6088c5-be78-494c-bb02-6374f033c875)


# Another VM for Minikube and kubectl and Argocd

# install minikube and kubectl 

```bash

Install Kubernetes on Ubuntu/Debian 
#### Install Docker First if Installed Skip these steps
sudo apt update
sudo apt install curl
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/trusted.gpg.d/docker.gpg
sudo add-apt-repository "deb [arch=$(dpkg --print-architecture)] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
sudo apt update
sudo apt -y install docker-ce docker-ce-cli containerd.io docker-compose-plugin docker-registry 
sudo usermod -aG docker $USER
newgrp docker

######### Install MiniKube (kubernetes platform)
curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube_latest_amd64.deb
ls
sudo dpkg -i minikube_latest_amd64.deb

minikube start --driver=docker --nodes=2
sudo snap install kubectl --classic
minikube kubectl -- get pods
kubectl cluster-info
kubectl get pods
minikube addons list
minikube dashboard &
kubectl get nodes
kubectl get pods -A

### install argo cd
kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml

to get password

kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d; echo

and portforward
kubectl port-forward svc/argocd-server -n argocd 8080:443

```
#  deploy your app  

![image](https://github.com/user-attachments/assets/f65f936c-8d06-4eed-8319-ea66b92c091d)


![image](https://github.com/user-attachments/assets/1733766f-663a-4b6f-8ce2-c82533448584)

![image](https://github.com/user-attachments/assets/54a72242-c0d7-457f-bf54-00daa92190c7)




### Done 
![image](https://github.com/user-attachments/assets/64b5a45b-84a8-4043-9a1a-840f037cf7fd)
