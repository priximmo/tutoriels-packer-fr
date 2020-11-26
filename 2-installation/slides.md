%title: PACKER
%author: xavki


# Packer : installation


<br>




```
export VER="1.6.0"
wget https://releases.hashicorp.com/packer/${VER}/packer_${VER}_linux_amd64.zip
```

<br>


```
sudo apt install unzip
sudo unzip packer_1.6.0_linux_adm64.zip -d /usr/local/bin
sudo chmod 755 /usr/local/bin/packer
```


