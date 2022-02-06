opopovich Infra repository

#One command ssh to someinternalhost

ssh -J appuser@62.84.116.239 appuser@10.128.0.30

#Connect from working machine to someinternalhost using alias

#Add to ~/.ssh/config

Bastion Host

Host bastion HostName 62.84.116.239

IdentityFile ~/.ssh/appuser

User appuser

SomeinternalHost

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

testapp_IP = 62.84.118.94 testapp_port = 9292

#Additional task for homework 6

yc compute instance create \ 

--name reddit-app \ 

--hostname reddit-app \ 

--memory=4 \ 

--create-boot-disk image-folder-id=standard-images,image-family=ubuntu-1604- lts,size=10GB \ 

--network-interface subnet-name=default-ru-central1-a,nat-ip-version=ipv4 \

--metadata serial-port-enable=1 \

--metadata-from-file user-data=metadata.yaml



# Домашнее задание № 7. Packer


Установили packer

brew tap hashicorp/tap brew install hashicorp/tap/packer

Создали сервисный аккаунт

yc iam service-account create --name $SVC_ACCT --folder-id $FOLDER_ID

Выдаем права

yc resource-manager folder add-access-binding --id $FOLDER_ID --role editor --service-account-id $ACCT_ID

Создаем ключ

yc iam key create --service-account-id $ACCT_ID --output /User/mini/key.json

Создаем ubuntu16.json,вносим builders и provisioners,создаем папку scripts и копируем скрипты,убираем из скриптов sudo

Валидируем полученный json

packer validate ./ubuntu16.json

Запускаем полученный json

packer build ./ubuntu16.json

Получаем ошибку

Quota limit vpc.networks.count exceeded

Удаляем все сети и подсети в каталоге infra

Получаем ошибку

Failed to find instance ip address: instance has no one IPv4 external address

Добавляем в конфиг строку

"use_ipv4_nat": "true"

Запускаем сборку, после сборки на основе нашего образа делаем VM

Дополнительно устанавливаем необходимые пакеты и проверяем что образ работает.

Создаем variables.json, добавляем в gitignore

Создаем variables.example.json

Создаем key.json похожий на боевой чтобы пройти автотесты

Terraform -1 homework

Deploy previously created with packer image
Add ssh keys to able to login to host without password
Add variable to parametrise deployment

Terraform -2 homework

Add modules

Parametrise name of instance

Ansible -1 homework

Install pip and ansible

Created playbook

After delete reddit directory recreated by ansible.

Ansible-2 homework

This is a hardest homework ever.

Created many playbooks

Changed packer provider to use ansible playbooks.

Checked all VM created succefully,app deployed and checked

Ansible-3 homework

Created roles,group_vars

Add community role jdauphant.nginx

Checked app available on port 80

Create ansible vault,encrypted credentials and created users.

Ansible-4 homework

Learn how to work with Vagrant,Vagrantfile

Deploy app in virtualbox via Vagrant

Try to config Nginx ( task with *)

Configure Molecule and run test

Write test to check mongodb port

Rewrite packer playbook
