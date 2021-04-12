echo -- mode: ruby --
echo vi: set ft=ruby :
require 'yaml'
yaml = YAML.load_file("core/machines.yml")

echo ENV
MYSQL_USER = "admdimdim"
MYSQL_ROOT_PASSWORD = "s8u7r$?eropAvuv"
MYSQL_PASSWORD = "@Fiap2tdst2021"
MYSQL_DATABASE = "db_fiap"
PMA_HOST= "192.168.66.20"
PMA_ARBITRARY = 1

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

if [ $HOSTNAME = "mysql-lab" ]; then
  echo 'ATUALIZANDO S.O'
  sudo apt update -y && sudo apt upgrade -y && sudo apt install wget -y
  echo 'BAIXANDO VERSAO DE MYSQL ESPECIFICADA NO PDF'
  wget -c https://dev.mysql.com/downloads/file/?id=500428
  echo 'INSTALANDO REPOSITORIO'
  sudo dpkg -i mysql-apt-config_0.8.16-1_all.deb
  echo 'BAIXANDO ATUALIZACOES PARA REPOSITORIOS'
  sudo apt-get update
  echo 'INSTALANDO PACOTE DO MYSQL-SERVER'
  sudo apt-get install mysql-server -y
  sleep 5
  echo 'INICIANDO MYSQL-SERVER'
  sudo systemctl start mysql
  echo 'SETANDO MYSQL PARA INICIAR JUNTO COM O S.O'
  sudo systemctl enable mysql
  echo 'CONFIGURAÇÕES INICIAIS DO MYSQL INLINE, ALTERANDO SENHA DO ROOT'
  sudo mysql -e "UPDATE mysql.user SET Password = PASSWORD('$MYSQL_ROOT_PASSWORD') WHERE User = 'root'"
  echo 'REMOVENDO ACESSO DO USUARIO ANONIMO CRIADO'
  sudo mysql -e "DROP USER ''@'localhost'"
  echo 'REMOVENDO USUARIO DEFAULT'
  sudo mysql -e "DROP USER ''@'$(hostname)'"
  echo 'REMOVENDO DATABASE TEST'
  sudo mysql -e "DROP DATABASE test"
  echo 'LIMPANDO PREVILEGIOS DEFAULT'
  sudo mysql -e "FLUSH PRIVILEGES"
  echo 'CRIANDO DATABASE'
  sudo mysql -e "CREATE DATABASE $MYSQL_DATABASE"
  echo 'PERMISSIONANDO USUARIO NA DATABASE'
  sudo mysql -e "GRANT ALL PRIVILEGES ON $MYSQL_DATABASE.* TO '$MYSQL_USER'@'localhost' IDENTIFIED BY '$MYSQL_PASSWORD'"

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
  echo 'EXECUTANDO CONTAINER DE WORDPRESS'
  docker run --env MYSQL_ROOT_PASSWORD=$MYSQL_ROOT_PASSWORD \
             --env MYSQL_DATABASE=$MYSQL_DATABASE \
             --env MYSQL_USER=$MYSQL_USER \
             --env MYSQL_PASSWORD=$MYSQL_PASSWORD \
             -it --name wordpress -p 8080:80 wordpress
  echo 'EXECUTANDO CONTAINER DE PHPMYADMIN'
  docker run --env PMA_HOST=$PMA_HOST \
             --env PMA_ARBITRARY=$PMA_ARBITRARY \
             -it --name phpmyadmin -p 8081:80 phpmyadmin

fi;
  date +"%H:%M:%S"
  sleep 5
SHELL

end
