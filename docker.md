### Docker ###

# Instalar o docker-compose no linux
sudo curl -L https://github.com/docker/compose/releases/download/1.21.2/docker-compose-$(uname -s)-$(uname -m) -o /usr/local/bin/docker-compose
chmod +x /usr/local/bin/docker-compose

# Tabela de compatibilidade do docker-compose com a versao do docker
https://docs.docker.com/compose/compose-file/compose-versioning/#compatibility-matrix

# Iniciar uma imagem do mysql
docker run --name=mysql --env="MYSQL_ROOT_PASSWORD=123456" -p 3306:3306 -d mysql:5.7
docker run --name=mysql-video -="MYSQL_ROOT_PASSWORD=123456, MYSQL_DATABASE=videocommerce” -p 3306:3306 -d mysql:5.7

# Ver todos containers ativos
docker ps

# Ver todos container incluindo os parados
docker ps -a

# Ver todas imagens
docker images

# Parar um container
docker stop CONTAINER_ID

# Remover um container parado
docker rm CONTAINER_ID

# Parar e remover um container ativo
docker rm -f CONTAINER_ID

# Remover uma imagem
docker rmi IMAGE_ID

# Remover uma imagem que está sendo utilizada e seus containers
docker rmi -f IMAGE_ID

# Remover todas as imagens que não estão sendo utilizadas
docker images -q |xargs docker rmi

# Criar uma imagem a partir do Dockerfile
docker build -t TAG:VERSAO .

# Iniciar um script do docker-compose
Obs.: se criar o arquivo docker-compose.yml com esse nome na raiz então não precisa passar como parâmetro no “-f”
docker-compose -f ARQUIVO.yml up -d

# Iniciar um script do docker-compose fazendo o rebuild dos serviços (quando se utilizar o Dockerfile)
docker-compose -f ARQUIVO.yml up -d —build

# Parar containers através de um script do docker-compose
docker-compose -f ARQUIVO.yml down

# Verificar as imagens do docker-compose
docker-compose images

# Verificar os logs de um container
docker logs CONTAINER_ID

# Verificar os logs de maneira contínua
docker logs -f CONTAINER_ID

# Acessar um docker
Docker exec -it CONTAINER_ID bash

# Fazer o rebuild de um serviço com alterações no Dockerfile
docker-compose down SERVICE_NAME
docker-compose build —no-cache SERVICE_NAME
docker-compose up -d

# Instalar pacotes básicos no docker para manutenção
apt-get update
apt-get install net-tools (netstat)
apt-get install iputils-ping
apt-get install mysql-client
apt-get install less
apt-get install wget