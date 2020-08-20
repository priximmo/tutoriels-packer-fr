%title: PACKER
%author: xavki


# PACKER : VBox - création via preseed


<br>


```
"/install/vmlinuz<wait>",									# localisation du noyau
" auto<wait>",
" console-setup/ask_detect=false<wait>",	# setting du keymap comme boot parameter
" console-setup/layoutcode=us<wait>",			# clavier azerty
" console-setup/modelcode=pc105<wait>",		# clavier
" debconf/frontend=noninteractive<wait>", # activation du mode non interactif (interface)
" debian-installer=fr_FR<wait>",					# langue de l'installer
" fb=false<wait>",												# non utilisation du frame buffer (tampon vidéo pour plusieurs langues)
" initrd=/install/initrd.gz<wait>",				# localisation de l'initrd
" kbd-chooser/method=fr<wait>",						# détection de keyboard
" keyboard-configuration/layout=FR<wait>",					# config du keyboard
" keyboard-configuration/variant=FR<wait>",					# config du keyboard
" locale=fr_FR<wait>",															# config des locales
" netcfg/get_domain={{user `domain`}}<wait>",				# config du domain
" netcfg/get_hostname={{user `hostname`}}<wait>",		# config du hostname
" grub-installer/bootdev=/dev/sda<wait>",						# localisation du MBR
" noapic<wait>",																		# désactivation de messages au boot (APIC = IRQ)
" preseed/url=http://{{ .HTTPIP }}:{{ .HTTPPort }}/preseed.cfg",  # localisation du preseed et type
" -- <wait>",
...
```


--------------------------------------------------------------------------


choose-mirror-bin mirror/http/proxy string   # vide = installation sans proxy
d-i base-installer/kernel/override-image string linux-server 	# installer la version du noyau du serveur
d-i clock-setup/utc boolean true							# réglage de l'horloge
d-i clock-setup/utc-auto boolean true					# réglage de l'horloge
d-i finish-install/reboot_in_progress note		# reboot après installation
d-i grub-installer/only_debian boolean true		# installation de grub sur le système d'amorçage principal
d-i grub-installer/with_other_os boolean true	# y compris si d'autres OS
d-i partman-auto/disk string /dev/sda					# utilisation du premier disque
d-i partman-auto-lvm/guided_size string max		# quelle taille pour le VG
d-i partman-auto/choose_recipe select atomic	# tout dans une seule partition (home > séparation, multi > var...)
d-i partman-auto/method string lvm						# utilisation de LVM standard (non encrypted)
d-i partman-lvm/confirm boolean true					# confirmation du choix LVM
d-i partman-lvm/confirm_nooverwrite boolean true # confirmation du choix d'écraser
d-i partman-lvm/device_remove_lvm boolean true	# si il y a des datas on confirme que l'on remove
d-i partman/choose_partition select finish			# partitioning sans confirmation
d-i partman/confirm boolean true								# confirmation	
d-i partman/confirm_nooverwrite boolean true		# confirmation
d-i partman/confirm_write_new_label boolean true # confirmation
d-i pkgsel/include string openssh-server cryptsetup build-essential libssl-dev libreadline-dev zlib1g-dev linux-source dkms nfs-common																							# paquets
d-i pkgsel/install-language-support boolean false # mise à jour langages
d-i pkgsel/update-policy select none 							# mise à jour policy
d-i pkgsel/upgrade select full-upgrade						# upgrade
d-i time/zone string UTC													# setting de la TZ
tasksel tasksel/first multiselect standard, ubuntu-server  # type d'installation (desktop, server...)

--------------------------------------------------------------------------

d-i console-setup/ask_detect boolean false 							 	# keyboard comme paramètre de boot
d-i keyboard-configuration/xkb-keymap select fr(latin9)		# type de keyboard
d-i keyboard-configuration/modelcode string pc105					# type de keyboard
d-i debian-installer/locale string fr_FR									# configuration des locales

# Create vagrant user account.
d-i passwd/user-fullname string vagrant
d-i passwd/username string vagrant
d-i passwd/user-password password vagrant
d-i passwd/user-password-again password vagrant
d-i user-setup/allow-password-weak boolean true
d-i user-setup/encrypt-home boolean false
d-i passwd/user-default-groups vagrant sudo
d-i passwd/user-uid string 900

