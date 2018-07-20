# Instalar o pacote subversion
apt-get install subversion

# Subir o servidor
svnserve -d --listen-host 10.61.64.4

#Criar um projeto novo
svnadmin create /projetos