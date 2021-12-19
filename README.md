# opopovich_infra
opopovich Infra repository

#One command ssh to someinternalhost

ssh -J appuser@62.84.116.239 appuser@10.128.0.30

#Connect from working machine to someinternalhost using alias

#Add to ~/.ssh/config

### Bastion Host

Host bastion
  HostName 62.84.116.239 
  
  IdentityFile ~/.ssh/appuser
  
  User appuser
  

### SomeinternalHost
Host someinternalhost

  HostName 10.128.0.30
  
  IdentityFile ~/.ssh/appuser
  
  User appuser
  
  ProxyJump bastion

bastion_IP = 62.84.116.239 

someinternalhost_IP = 62.84.116.239

#Additional task add letsencrypt cert to pritunl web server

#Install certbot via snapd 

sudo apt install snapd
sudo snap install core; sudo snap refresh core
sudo snap install --classic certbot

#and add this line in field LetsEncrypt certificate in Settings section

62.84.116.239.sslip.io

