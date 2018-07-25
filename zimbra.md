#Comandos Zimbra

#Limpar pasta
zmmailbox -z -m copia@rolamentosradial.com.br emptyFolder /Inbox
#Alterar página de logout
zmprov mcf zimbraWebClientLogoutURL http://webmail.vm10.com.br
#Configurações de IP do SMTP e Proxy
zmprov mcf zimbraMtaRelayHost 10.14.78.132:27
zmprov mcf zimbraSmtpHostname 10.14.78.132
zmprov ms mail02.vm10.com.br zimbraMtaMyDestination 10.14.78.132
zmprov ms mail02.vm10.com.br zimbraMtaRelayHost 10.14.78.132
zmprov ms mail02.vm10.com.br zimbraSmtpHostname 10.14.78.132
zmprov ms mail04.vm10.com.br zimbraSmtpPort 27
#Inicializar pasta Documentos
zmprov in wiki@z1.cti.com.br
zmprov ut -h z1.cti.com.br /opt/zimbra/wiki/Template/
#Iniciar LDAP do Zimbra
sudo /opt/zimbra/openldap/libexec/slapd  -l LOCAL0 -4 -u zimbra -h ldap://mail.vm10.com.br:389/ -f /opt/zimbra/conf/slapd.conf
#Pegar senha do mysql do zimbra
su - zimbra
zmlocalconfig -s | grep mysql | grep password
#Pegar socket do mysql
netstat -lnp |grep mysql
#Exportar uma tabela do mysql do Zimbra
mysqldump -S /opt/zimbra/db/mysql.sock zimbra --tables config -p (Tem que estar como root, a senha é a mysql_root_password)
#Acessar o mysql do Zimbra
su - zimbra
mysql zimbra
# Backup do banco do Zimbra
mysqldump -S /opt/zimbra/db/mysql.sock zimbra -p > /tmp/mysql_zimbra.bkp
# Importar backup no banco do zimbra
mysql -S /opt/zimbra/db/mysql.sock zimbra -p < /tmp/config.bkp (como root, pegar a senha conforme linha abaixo)
zmlocalconfig -s | grep mysql | grep mysql_root_password (como zimbra, pegar a senha para rodar o comando acima)
 
#Alterar arquivos antes de subir o backup do mail
cd /opt/zimbra/jetty/etc
sed 's/74.86.196.27/10.14.78.138/g' jetty.xml.in > jetty.xml.in.novo;  mv jetty.xml.in.novo jetty.xml.in
sed 's/74.86.196.27/10.14.78.138/g' zimbra.web.xml.in > zimbra.web.xml.in.novo;  mv zimbra.web.xml.in.novo zimbra.web.xml.in
 
#Exportar conta
zmmailbox -z -m conta@dominio.com.br getRestURL '//?fmt=tgz&query=is:anywhere' > /tmp/conta@dominio.com.br.tgz
 
#Importar conta sem apagar o conteúdo atual
zmmailbox -z -m conta@dominio.com.br  postRestURL '//?fmt=tgz&resolve=skip' ./conta@dominio.com.br.tgz
#Importar conta apagando o conteúdo existente
zmmailbox -z -m conta@dominio.com.br  postRestURL '//?fmt=tgz&resolve=reset' ./conta@dominio.com.br.tgz
 
#Importar email de um store para a conta (para trazer a data, rode o script zimdates antes que está no mail)
zmlmtpinject -r conta@cominio.com.br -N 50 -d pasta
 
#Configurar catálogo de endereços LDAP
zmprov md helipark.net zimbraGalLdapBindDn cn=config
zmprov md helipark.net zimbraGalLdapBindPassword zi2m3ldap
zmprov md helipark.net zimbraGalLdapFilter "(|(cn=*%s*)(sn=*%s*)(gn=*%s*)(mail=*%s*))"
zmprov md helipark.net zimbraGalAutoCompleteLdapFilter "(|(cn=%s*)(sn=%s*)(gn=%s*)(mail=%s*))"
zmprov md helipark.net zimbraGalLdapSearchBase "dc=helipark.net"
zmprov md helipark.net zimbraGalLdapURL "ldap://ldap.vm10.com.br:389"
zmprov md helipark.net zimbraGalMode ldap
 
#Configurar resposta automática
zmprov ma demo@vm10.com.br zimbraPrefOutOfOfficeReplyEnabled TRUE
zmprov ma demo@vm10.com.br zimbraPrefOutOfOfficeReply "FERIAS COLETIVAS
Informamos aos nossos clientes, fornecedores e colaboradores
que estaremos em ferias coletivas no periodo de
19/12/2011 a 02/01/2012.
Retornaremos em 03/01/2012 (terca-feira)
Desejamos a todos BOAS FESTAS"
zmprov ma demo@vm10.com.br zimbraPrefOutOfOfficeFromDate 20111219030000Z
zmprov ma demo@vm10.com.br zimbraPrefOutOfOfficeUntilDate 20120102030000Z