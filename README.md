# Learning NGINX

This is my personal journey learning NGINX ;-)

## Create a Virtual Machine (VM) on Azure

Let's first create a _resource group_:

```text
az group create --name pk-experiment-01 --location westeurope
```

Then, we can create a VM _resource_ within the _resource group_:

```text
az vm create \
  --resource-group pk-experiment-01 \
  --name pk-experiment-01-vm-01 \
  --image UbuntuLTS \
  --admin-username radicel \
  --generate-ssh-keys \
  --public-ip-sku Standard
```

We need to make sure that the port 80 is open:

```text
az vm open-port --port 80 --resource-group pk-experiment-01 --name pk-experiment-01-vm-01
```

You can retrieve the public IP address of your VM with the following command:

```text
az vm show --resource-group pk-experiment-01 --name pk-experiment-01-vm-01 --show-details | jq .publicIps
```

## Install NGINX

First, connect to your VM via SSH:

```text
ssh radicel@192.0.2.3
```

where you have to replace `192.0.2.3` by the public IP address of the Azure VM.

Then, you can install **NGINX**:

```text
radicel@pk-experiment-01-vm-01:~$ sudo apt-get update
radicel@pk-experiment-01-vm-01:~$ sudo apt-get -y upgrade
radicel@pk-experiment-01-vm-01:~$ sudo apt-get -y install nginx
radicel@pk-experiment-01-vm-01:~$ exit
```

And test the installation with your browser or `curl`:

```text
curl 192.0.2.3
```

where you have to replace `192.0.2.3` by the public IP address of the Azure VM.

At the end, you can remove **all** the resources in **one go** with the following command:

```text
az group delete --name pk-experiment-01
```
