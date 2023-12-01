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

Open Remote Desktop Connection and type the Azure VM Public IP address 
and the username "azureuser" and then press connect.

Then enter the password to access the Linux GUI Desktop

---------------------------------------------------------------------------------------------------------------------------
HOW TO INSTALL VSCODE
---------------------------------------------------------------------------------------------------------------------------

sudo apt install software-properties-common apt-transport-https wget
wget -q https://packages.microsoft.com/keys/microsoft.asc -O- | sudo apt-key add -
sudo add-apt-repository "deb [arch=amd64] https://packages.microsoft.com/repos/vscode stable main"
sudo apt update
sudo apt install code

---------------------------------------------------------------------------------------------------------------------------
HOW TO INSTALL GOOGLE CHROME
---------------------------------------------------------------------------------------------------------------------------

wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb
sudo dpkg -i google-chrome-stable_current_amd64.deb



---------------------------------------------------------------------------------------------------------------------------
HOW TO INSTALL .NET 8 SDK
---------------------------------------------------------------------------------------------------------------------------

wget https://packages.microsoft.com/config/ubuntu/20.04/packages-microsoft-prod.deb -O packages-microsoft-prod.deb
sudo dpkg -i packages-microsoft-prod.deb


sudo apt update
sudo apt install -y apt-transport-https
sudo apt update
sudo apt install -y dotnet-sdk-8.0

dotnet --version
