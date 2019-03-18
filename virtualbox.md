# Adicionar placa de rede para acessar a VM via SSH

## Adicionar uma segunda placa de rede ao serivdor virtual
- Abrir o geranciador do VirtualBox
- Selecione o servidor desejado
- Clique no menu Máquina / Configurações
- Cliente em Rede
- Deixe o primeiro adaptador como "NAT" (permite que a vm acesse a internet)
- Adiciona um segundo adaptador como "Placa de rede exclusiva de hospedeiro (host-only)"

## Configurando a placa de rede no linux
- Acesse o terminal da VM
- ifconfig (Lista todas as conexões ativas)
- ifconfig -a (Lista todas as conexões, incluíndo a placa que foi adicionada e ainda não está configurada)
- Abrir o arquivo de interfaces para editar
> `vi /etc/network/interfaces`

- Adicionar a configuração da placa de rede nova
```sh
# Placa de rede para acessar via SSH
auto enp0s8
iface enp0s8 inet static
address 192.168.56.2
netmask 255.255.255.0
```
- Iniciar a placa de rede configurada
```sh
# Instalar pacote para reiniciar subir a placa
sudo apt-get install ifupdown
# Iniciar a placa nova
sudo ifup enp0s8
```

## Fontes
https://code-maven.com/virtualbox-host-only-network-ssh-to-remote-machine


