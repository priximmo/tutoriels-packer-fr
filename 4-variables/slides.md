%title: PACKER
%author: xavki


# PACKER : Variables


<br>


* les variables packer par bloc json "variables

```
  "variables": {
    "mavariables": "mavaleur",
  }
```

<br>


* les variables la CLI -var ou -var-file

```
packer build -var 'aws_access_key=foo'
```

<br>


* ex : fichier de variables json

```
{
  "aws_access_key": "foo",
  "aws_secret_key": "bar"
}
```

---------------------------------------------------------------------------------

# PACKER : Provisionner Variables


<br>


* pour les utiliser

```
user `mavariable`
```

* sur tout le template sauf dnas le bloc variables

Rq : ausi variables issues de vault, consul, aws_secretmanager

<br>


* packer inspect pour y voir plus clair

```
packer inspect ubuntu.json
```

<br>


* sensitive variables > logs

```
{
  "variables": {
    "my_secret": "{{env `MY_SECRET`}}",
    "not_a_secret": "plaintext",
    "foo": "bar"
  },

  "sensitive-variables": ["my_secret", "foo"],
  ...
}
```

<br>


* poser des conditions

```
  "provisioners": [{
    "type": "shell",
    "inline": [
    "if [ ! -z '{{ user `valeur_cond`}}' ]; then echo '{{ user `valeur_cond`}}' > hello.txt; fi"
    ]
  }],

```

doc : https://www.packer.io/docs/templates/user-variables.html
