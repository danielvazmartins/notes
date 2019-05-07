# Comandos úteis
```bash
# Verificar versão do ubuntu
lsb_release -a
```
 
# Certificado digital
```bash
# Gerar requisição de certificado
openssl genrsa -des3 -out exchange.vm10.com.br.key 2048
openssl req -new -key exchange.vm10.com.br.key -out exchange.vm10.com.br.csr
 
# Conferir arquivo de requisição
openssl req -in m.efacil.com.br.csr -noout -text
 
# Converter o certificado para .pfx
openssl pkcs12 -export -out webmail.sultransporte.com.br.pfx -inkey webmail.sultransporte.com.br.key -in webmail.sultransporte.com.br.crt
 
# Converter key para o formato rsa
openssl rsa -in server.key -out server.key.rsa
ou
openssl rsa -in drogasil.key.pem -outform pem
 
# Remover a senha do certificado
openssl rsa -in file.key -out newfile.key
 
# Extrair o crt e a key do pfx
#Note: the *.pfx file is in PKCS#12 format and includes both the certificate and the private key.
#Run the following command to export the private key:
openssl pkcs12 -in certname.pfx -nocerts -out key.pem -nodes
#Run the following command to export the certificate:
openssl pkcs12 -in certname.pfx -nokeys -out cert.pem
#Run the following command to remove the passphrase from the private key:
openssl rsa -in key.pem -out server.key
Ex.:
openssl pkcs12 -in m.extra.com.br.pfx -nocerts -out m.extra.com.br.key.pass -nodes
openssl pkcs12 -in m.extra.com.br.pfx -nokeys -out m.extra.com.br.crt
openssl rsa -in m.extra.com.br.key.pass -out m.extra.com.br.key
 
# Validar certificado
openssl x509 -noout -modulus -in m.cdiscount.com.br.crt | openssl md5
openssl rsa -noout -modulus -in m.cdiscount.com.br.key | openssl md5
openssl req -noout -modulus -in m.cdiscount.com.br.csr | openssl md5
```

# SSH
```bash
# Gerar chaves no linux e copiar para o host de destino
ssh-keygen -t rsa
ssh-copy-id -i /root/.ssh/id_rsa.pub root@10.14.78.132
eval `ssh-agent`
ssh-add

# Gerar chaves no Windows e salvar no host de destino
- Utilizar o puttygen para gerar o par de chaves
C:\Program Files\PuTTY\puttygen.exe
- Clicar em generate para gerar as chaves
- Copiar a public key gerada na tela (ssh-rsa XXXXX...)
- Adicionar a public key no arquivo ~/.ssh/authorized_keys do host
- Salvar a private key (nome-rsa-private.ppk)
- Utilizar a private key no putty para acessar o host sem senha
```

# Adicionando Swap no Ubuntu 16.04
```bash
swapon --show
fallocate -l 1G /swapfile
chmod 600 swapfile
mkswap /swapfile
swapon /swapfile
swapon --show
sysctl vm.swappiness=10
sysctl vm.vfs_cache_pressure=50

# Fonte
https://www.digitalocean.com/community/tutorials/how-to-add-swap-space-on-ubuntu-16-04
```


# Monitorar fila do postfix
watch -n1 'postqueue -p |tail -n 1'

# Executar o logrotate manualmente
logrotate --force $CONFIG_FILE

# Adicionar biblioteca no classpath do JAVA
export CLASSPATH=/usr/local/jetty-6.1.19/lib/mail-1.4.jar:.

# Pacotes úteis
netcat-openbsd - TCP/IP swiss army knife
tcpdump - command-line network traffic analyzer
traceroute - Traces the route taken by packets over an IPv4/IPv6 network
mtr - Full screen ncurses and X11 traceroute tool