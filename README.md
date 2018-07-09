# learning-nginx

My personal journey learning NGINX ;-)

## Create a Virtual Machine (VM) on Azure

Let's create an **Azure VM** of size *Standard D2s v3 (2 vcpus, 8 GB memory)*:

  ```command
  user@Azure:~$ az group create --name experiment-01 --location francecentral
  user@Azure:~$ az vm create \
    --resource-group experiment-01 \
    --name node-01 \
    --image UbuntuLTS \
    --size Standard_D2s_v3 \
    --admin-username radicel \
    --generate-ssh-keys
  user@Azure:~$ az vm open-port --port 80 --resource-group experiment-01 --name node-01
  user@Azure:~$ ssh radicel@PublicIPAddress
  ```

Then we can install **NGINX**:

  ```command
  radicel@minikube-01:~$ sudo apt-get -y update
  radicel@minikube-01:~$ sudo apt-get -y install nginx
  radicel@minikube-01:~$ exit
  ```

At the end, you can remove **all** the resources in **one go** with the following command:

```command
  user@Azure:~$ az group delete --name experiment-01
```
