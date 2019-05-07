# Atualizar hora automaticamento com o NTP

```bash
# instalar os pacotes necessários
apt-get update
apt-get install ntp
service ntp start

timedatectl set-timezone America/Sao_Paulo
```

## Fontes
https://ntp.br/guia-linux-avancado.php
https://www.digitalocean.com/community/tutorials/how-to-configure-ntp-for-use-in-the-ntp-pool-project-on-ubuntu-16-04
https://www.digitalocean.com/community/tutorials/how-to-set-up-timezone-and-ntp-synchronization-on-ubuntu-14-04-quickstart