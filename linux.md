# Executar o logrotate manualmente
logrotate --force $CONFIG_FILE

# Verificar vers„o do ubuntu
lsb_release -a
 
# Gerar Certificado
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
 
#Monitorar fila do postfix
watch -n1 'postqueue -p |tail -n 1'
 
# Gera chaves e copia para o host de destino
ssh-keygen -t rsa
ssh-copy-id -i /root/.ssh/id_rsa.pub root@10.14.78.132
eval `ssh-agent`
ssh-add
 
# Adicionar biblioteca no classpath do JAVA
export CLASSPATH=/usr/local/jetty-6.1.19/lib/mail-1.4.jar:.