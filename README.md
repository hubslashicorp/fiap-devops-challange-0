![UML](img/LogotipoSlashicorp.png)

# FIAP Challange DevOps - Part I

Em nosso `lab`, para estudar `Linux` e `Docker`, provisionaremos uma VM `Ubuntu-server` no `VirtualBox` com o `Vagrant`.
 
Caso você rode `Windows`, não se preocupe! Também é possivel rodar o terminal `Linux` nele com o `wsl`:

```
Instalando wsl: https://docs.microsoft.com/pt-br/windows/wsl/install-win10
```

No nosso, caso utilizaremos o `VirtualBox` sendo assim, de qualquer maneira você pode participar pois, `VirtualBox`, `Vagrant` e o `Docker` rodam no `Windão`.
 
## PRE-RECs:

Para clonar o nosso repositorio voce precisara instalar o GIT em sua estaçã de trabalho

Instalando Git:
``` 
 https://git-scm.com/book/en/v2/Getting-Started-Installing-Git
```

Instalando VirtualBox:
```
Download: https://www.virtualbox.org/wiki/Downloads
Documentacão: https://www.virtualbox.org/wiki/Documentation
```

Instalando Vagrant:
```
Download: https://www.vagrantup.com/downloads.html
Documentacão: https://www.vagrantup.com/docs
Boxes: https://app.vagrantup.com/boxes/search
```

Caso queira iniciar o server diretamente sem utilizar Vagrant Ubuntu 18.04 LTS (ISO)
```
Download: https://ubuntu.com/download/server
Documentacão: https://help.ubuntu.com/
```

Instalando Docker
``` 
Download: https://docs.docker.com/engine/install/ubuntu/
Docker Hub: https://hub.docker.com/
```

## Observação importante:

Em alguns casos o download da `box` Vagrant demora uma eternidade para baixar sendo assim,
caso queira provisionar o ambiente com antecedencia, apos instalar o Git, Virtualbox e o Vagrant, navegue ate o 
repositorio clonado localmente em sua maquina e execute os passos:

1.0 - Realize o clone do repositorio:
```
$ git clone https://github.com/hubslashicorp/fiap-devops-challange-0.git
```

2.0 - Acesse o diretório local `fiap-devops-challange-0`:
``` 
$ cd fiap-devops-challange-0
```

## Estrutura do diretório:

```
.
├── README.md
├── Vagrantfile
├── core
│   └── machines.yml
└── img
    └── LogotipoSlashicorp.png
```

3.0 - Provisionando VM com Vagrant:
``` 
$ vagrant up
```

4.0 - Validando se VM esta Online:
``` 
$ vagrant status
```

5.0 - Desligando VM (`opcional`):
```
$ vagrant halt
```

6.0 - Destruindo a VM (`opcional`):
```
$ vagrant destroy
```
