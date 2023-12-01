# How to create an Azure Virtual Machine with Ubuntu Server and with a GUI Desktop

## 1. INSTALL AND CONFIGURE xrdp TO USE REMOTE DESKTOP WITH UBUNTU

https://learn.microsoft.com/en-us/azure/virtual-machines/linux/use-remote-desktop?tabs=azure-cli

1.1. Create an Azure Virtual Machine with Ubuntu Server installed

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
