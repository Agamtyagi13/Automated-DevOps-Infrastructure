
docker -
 
 sudo apt-get update
 sudo apt-get install docker.io -y
 sudo systemctl enable docker
sudo systemctl start docker
sudo usermod -aG docker $USER
newgrp docker

kubectl -

curl -LO "https://dl.k8s.io/release/$(curl -L -s \
https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"

chmod +x kubectl

sudo mv kubectl /usr/local/bin/

kind -

curl -Lo ./kind https://kind.sigs.k8s.io/dl/latest/kind-linux-amd64

chmod +x kind

sudo mv kind /usr/local/bin/

kind create cluster --name devops

kubectl get nodes

helm -

curl -fsSL -o get_helm.sh https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3
chmod 700 get_helm.sh
./get_helm.sh

argo cd -


kubectl create namespace argocd

kubectl apply -n argocd \
-f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml

kubectl port-forward svc/argocd-server \
-n argocd 8080:443

kubectl -n argocd get secret argocd-initial-admin-secret \
-o jsonpath="{.data.password}" | base64 -d


Prometheus and Grafana -


helm repo add prometheus-community \
https://prometheus-community.github.io/helm-charts

helm repo update

kubectl create namespace monitoring

helm install monitoring \
prometheus-community/kube-prometheus-stack \
-n monitoring

kubectl port-forward svc/monitoring-grafana \
3000:80 -n monitoring

kubectl get secret monitoring-grafana \
-n monitoring \
-o jsonpath="{.data.admin-password}" | base64 -d

kubectl port-forward \
svc/monitoring-kube-prometheus-prometheus \
9090:9090 -n monitoring

Jenkins

sudo apt update
sudo apt install fontconfig openjdk-21-jre -y
java -version


sudo wget -O /usr/share/keyrings/jenkins-keyring.asc \
https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key

echo "deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
https://pkg.jenkins.io/debian-stable binary/" | \
sudo tee /etc/apt/sources.list.d/jenkins.list > /dev/null

sudo apt update
sudo apt install jenkins -y

sudo systemctl enable jenkins
sudo systemctl start Jenkins


sudo cat /var/lib/jenkins/secrets/initialAdminPassword


aws cli-


sudo apt update
sudo apt install unzip curl -y

curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
unzip awscliv2.zip
sudo ./aws/install

aws configure

SonarQube -


docker run -d \
  --name sonarqube-server \
  -p 9000:9000 \
  sonarqube:lts-community


trivy -

sudo apt install wget apt-transport-https gnupg lsb-release -y


wget -qO - https://aquasecurity.github.io/trivy-repo/deb/public.key | \
gpg --dearmor | \
sudo tee /usr/share/keyrings/trivy.gpg > /dev/null


echo "deb [signed-by=/usr/share/keyrings/trivy.gpg] \
https://aquasecurity.github.io/trivy-repo/deb \
$(lsb_release -cs) main" | \
sudo tee /etc/apt/sources.list.d/trivy.list


sudo apt update

sudo apt install trivy -y


AMAZON Q CLI

sudo apt update
sudo apt install -y libfuse2

curl --proto '=https' --tlsv1.2 -sSf https://desktop-release.q.us-east-1.amazonaws.com/latest/amazon-q.deb -o amazon-q.deb


sudo apt install -y ./amazon-q.deb
