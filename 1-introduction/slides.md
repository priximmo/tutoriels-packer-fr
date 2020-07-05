%title: PACKER
%author: xavki


# PACKER : introduction


<br>
* outil hashicorp : vagrant, terraform, nomad, consul, vault...

<br>
* construction d'image pour machine virtuelle
		* packer > terraform > ansible
		* packer > ansible > terraform > ansible

<br>
* processus de templating

<br>
* personnalisation : durcissement/sécurité, utilisateurs, conf ssh, préconfiguration (gagner du temps)...
		* CPU/RAM
		* datastore
		* volumétrie
		* iso source
		* preseed...

<br>
* en fonction des principales destinations :
			* AWS
			* GCP
			* Azure
			* Docker / LXD / LXC
			* VirtualBox
			* VMWare
			* Openstack
			* Scaleway
			* Proxmox
			* Alicloud

----------------------------------------------------------------------------------

# PACKER : introduction

<br>
* Défintions :

<br>
		* artifacts : une image résultant d'un build packer (suivant la destination)

<br>
		* builds : c'est une tâche packer

<br>
		* builders : outils de création de l'image spécifique à sa destination

<br>
		* post-processor : action réalisée après la production de l'image (push...)

<br>
		* template : fichier au format json qui décrit l'image et sa production

<br>
		* variables 
