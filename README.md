# How to create an Azure Virtual Machine with Ubuntu Server and with a GUI Desktop

## 1. INSTALL AND CONFIGURE xrdp TO USE REMOTE DESKTOP WITH UBUNTU

https://learn.microsoft.com/en-us/azure/virtual-machines/linux/use-remote-desktop?tabs=azure-cli

1.1. Create an Azure Virtual Machine with Ubuntu Server installed

![image](https://github.com/luiscoco/Azure_VM_Ubuntu_with_GUI_Desktop/assets/32194879/be25dbb5-736f-4ad6-a0cd-82693eebdc91)

![image](https://github.com/luiscoco/Azure_VM_Ubuntu_with_GUI_Desktop/assets/32194879/7f92bef9-21f1-4278-ac71-4ff518f1dc75)

![image](https://github.com/luiscoco/Azure_VM_Ubuntu_with_GUI_Desktop/assets/32194879/8352c935-cc17-4a3d-adbf-ff08f2f2da5d)

![image](https://github.com/luiscoco/Azure_VM_Ubuntu_with_GUI_Desktop/assets/32194879/22e6405b-10cc-458d-9a71-f240c61c8047)

![image](https://github.com/luiscoco/Azure_VM_Ubuntu_with_GUI_Desktop/assets/32194879/ea08f29b-60b6-49fe-98a0-3dd3aaaa9861)

![image](https://github.com/luiscoco/Azure_VM_Ubuntu_with_GUI_Desktop/assets/32194879/ea97cdcd-45e2-46ab-aa24-c121e1dc98b9)

![image](https://github.com/luiscoco/Azure_VM_Ubuntu_with_GUI_Desktop/assets/32194879/15f44191-1eff-4c8c-b5b5-783b370443a4)

![image](https://github.com/luiscoco/Azure_VM_Ubuntu_with_GUI_Desktop/assets/32194879/e0be8705-9653-4608-bd90-7943b79d53bd)

![image](https://github.com/luiscoco/Azure_VM_Ubuntu_with_GUI_Desktop/assets/32194879/7c006411-5f42-43a2-a359-4a8dcf7f1b75)

![image](https://github.com/luiscoco/Azure_VM_Ubuntu_with_GUI_Desktop/assets/32194879/75b52d2e-cfb9-45cb-af65-38514f1aea91)

![image](https://github.com/luiscoco/Azure_VM_Ubuntu_with_GUI_Desktop/assets/32194879/2299dec1-ee14-4eae-8cef-118c683aba2a)

![image](https://github.com/luiscoco/Azure_VM_Ubuntu_with_GUI_Desktop/assets/32194879/f0c4c249-492b-475f-8bdb-cb79a18d9c3a)

Open a command prompt window and type the commands to access into the Linux VM:

```
az ssh vm --ip 20.61.2.228
```

![image](https://github.com/luiscoco/Azure_VM_Ubuntu_with_GUI_Desktop/assets/32194879/a35eb913-d3de-4932-ada9-590257c31c8f)

1.2. Run these commands to stall "xfce" using "apt":

```bash
sudo apt-get update
sudo DEBIAN_FRONTEND=noninteractive apt-get -y install xfce4
sudo apt install xfce4-session
```

1.3. Install and configure a remote desktop server:

```bash
sudo apt-get -y install xrdp
sudo systemctl enable xrdp
sudo adduser xrdp ssl-cert
echo xfce4-session >~/.xsession
sudo service xrdp restart
```

1.4. Set a local user account password

```bash
sudo passwd azureuser
```

## 2. HOW TO CREATE A NEW INBOUND RULE FOR THE REMOTE DESKTOP CONNECTION

```bash
az vm open-port --resource-group mylinuxvm1974_group --name mylinuxvm1974 --port 3389
```

## 3. OPEN REMOTE DESKTOP CONNECTION

Open Remote Desktop Connection and type the Azure VM Public IP address and the username "azureuser" and then press connect:

![image](https://github.com/luiscoco/Azure_VM_Ubuntu_with_GUI_Desktop/assets/32194879/b1d97b46-f61a-4b84-9ea2-6fb2077df1db)

Then enter the password to access the Linux GUI Desktop

![image](https://github.com/luiscoco/Azure_VM_Ubuntu_with_GUI_Desktop/assets/32194879/88da3f7f-0f29-449f-8f81-ecb7dffe64ce)

![image](https://github.com/luiscoco/Azure_VM_Ubuntu_with_GUI_Desktop/assets/32194879/d881368c-7876-4c09-851a-7e660470ae83)

### 3.1. HOW TO INSTALL VSCODE

Open a Terminal Emulator window and run the following commands to install the VSCode application

![image](https://github.com/luiscoco/Azure_VM_Ubuntu_with_GUI_Desktop/assets/32194879/98e76ee1-5832-4536-9692-babdce81e9ad)

```bash
sudo apt install software-properties-common apt-transport-https wget
wget -q https://packages.microsoft.com/keys/microsoft.asc -O- | sudo apt-key add -
sudo add-apt-repository "deb [arch=amd64] https://packages.microsoft.com/repos/vscode stable main"
sudo apt update
sudo apt install code
```

### 3.2. HOW TO INSTALL GOOGLE CHROME

```bash
wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb
sudo dpkg -i google-chrome-stable_current_amd64.deb
```


### 3.3. HOW TO INSTALL .NET 8 SDK

```bash
wget https://packages.microsoft.com/config/ubuntu/20.04/packages-microsoft-prod.deb -O packages-microsoft-prod.deb
sudo dpkg -i packages-microsoft-prod.deb

sudo apt update
sudo apt install -y apt-transport-https
sudo apt update
sudo apt install -y dotnet-sdk-8.0

dotnet --version
```
