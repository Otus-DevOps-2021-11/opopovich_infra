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
#Install certbot and add this line in field LetsEncrypt certificate
62.84.116.239.sslip.io

testapp_IP = 62.84.118.94 
testapp_port = 9292

#Additional task for homework 6

yc compute instance create \ 
--name reddit-app \ 
--hostname reddit-app \ 
--memory=4 \ 
--create-boot-disk image-folder-id=standard-images,image-family=ubuntu-1604- 
lts,size=10GB \ 
--network-interface subnet-name=default-ru-central1-a,nat-ip-version=ipv4 \ 
--metadata serial-port-enable=1 \
--metadata-from-file user-data=metadata.yaml

Terraform -1 homework

1. Deploy previously created with packer image
2. Add ssh keys to able to login to host without password
3. Add variable to parametrise deployment


