Installing Minikube on Ubuntu 20.04 LTS

=========================Installing Docker on Ubuntu 20.04 LTS===================================

Step 1: Updating system packages

```
sudo apt update 
```

```
sudo apt install apt-transport-https curl
```

Step 2. Installing Docker
```
sudo apt install docker.io
```
Step 3. Installing Docker’s service
```
sudo systemctl enable docker
```
```
sudo systemctl start docker
```
Step 4. Verifying Docker installation
```
docker --version
```
Docker version 20.10.21, build 20.10.21-0ubuntu1~20.04.2

=========================Installing Minikube on Ubuntu 20.04 LTS===================================

Step 5. Updating system packages and installing Minikube dependencies
```
sudo apt update
```
```
sudo apt install -y curl wget apt-transport-https
```
Step 6. Installing Minikube
```
curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
```
```
sudo install minikube-linux-amd64 /usr/local/bin/minikube
```
```
minikube version
```
minikube version: v1.32.0
commit: 8220a6eb95f0a4d75f7f2d7b14cef975f050512d

Step 7. Installing kubectl utility
```
curl -LO https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl
```
```
chmod +x kubectl
```
```
sudo mv kubectl /usr/local/bin/
```
Now, verify the kubectl version

```
kubectl version -o yaml
```
clientVersion:
 buildDate: "2023–11–15T16:58:22Z"
 compiler: gc
 gitCommit: bae2c62678db2b5053817bc97181fcc2e8388103
 gitTreeState: clean
 gitVersion: v1.28.4
 goVersion: go1.20.11
 major: "1"
 minor: "28"
 platform: linux/amd64
kustomizeVersion: v5.0.4–0.20230601165947–6ce0bf390ce3
serverVersion:
 buildDate: "2023–10–18T11:33:18Z"
 compiler: gc
 gitCommit: a8a1abc25cad87333840cd7d54be2efaf31a3177
 gitTreeState: clean
 gitVersion: v1.28.3
 goVersion: go1.20.10
 major: "1"
 minor: "28"
 platform: linux/amd64
 
Step 8. Starting Minikube
```
minikube start --driver=docker --force
```
```
minikube start --nodes 2 -p multinode-demo --driver=docker --force
```
Step 9. Verifying Installation
```
minikube status
```
minikube
type: Control Plane
host: Running
kubelet: Running
apiserver: Running
kubeconfig: Configured

```
alias k=kubectl                         # will already be pre-configured
```
```
export do="--dry-run=client -o yaml"    # k get pod x $do
```
```
export now="--force --grace-period 0"   # k delete pod x $now
```
| BUG  | FIX |
| ------------- | ------------- |
| Failed to start docker container. Running "minikube delete" may fix it: boot lock: unable to open /tmp/juju-mke11f63b5835bf422927bf558fccac7a21a838f: permission denied  | ``` minikube delete ```  |
| Error response from daemon: network 5e7828cee7f6faa0303467f726b1ed7f8cd9e01c6b00ecb954fa490bc3086851 not found Error: failed to start containers: multinode-demo-m02  | ``` minikube delete -p multinode-demo ```  |
| unable to open /tmp/juju-mkb814c315fe9b7fabb439d6d58c5448fbb7853c: permission denied | ``` chmod 777 /tmp/ ```  |





Link ref:
https://medium.com/@areesmoon/installing-docker-on-ubuntu-20-04-lts-focal-fossa-be807a50d16f
https://medium.com/@areesmoon/installing-minikube-on-ubuntu-20-04-lts-focal-fossa-b10fad9d0511
