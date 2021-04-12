# -- mode: ruby --
# vi: set ft=ruby :
require 'yaml'
yaml = YAML.load_file("core/machines.yml")

Vagrant.configure("2") do |config|
  yaml.each do |server|
    config.vm.define server["name"] do |srv|
      srv.vm.box = server["sistema"]
      srv.vm.network "private_network", ip: server["ip"]
      srv.vm.hostname = server["hostname"]
      srv.vm.provider "virtualbox" do |vb|
        vb.name = server["name"]
        vb.memory = server["memory"]
        vb.cpus = server["cpus"]
      end
  end
end

config.vm.provision "shell", inline: <<-SHELL

if [ $HOSTNAME = "devops-lab" ]; then
  echo 'ATUALIZANDO S.O'
  sudo apt update -y && sudo apt upgrade -y && sudo apt install wget -y
  echo 'BAIXANDO SCRIPT DE INSTALACAO DO DOCKER'
  curl -fsSL https://get.docker.com -o get-docker.sh
  echo 'EXECUTANDO SCRIPT DE INSTALACAO DOCKER'
  sudo sh get-docker.sh
  echo 'DANDO PREVILEGIOS AO GRUPO DOCKER PARA USUARIO VAGRANT'
  sudo usermod -a -G docker vagrant
  echo 'INICIANDO DOCKER'
  sudo systemctl start docker
  echo 'SETANDO DOCKER PARA INICIAR JUNTO COM O S.O'
  sudo systemctl enable docker
fi;
  date +"%H:%M:%S"
  sleep 5
SHELL

end
