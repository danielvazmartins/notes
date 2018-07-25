#Comandos Sharepoint

#Comando para corrigir o WSS depois de atualizar
stsadm -o upgrade -inplace -forceupgrade
#Fazer backup do site
stsadm -o backup -url http://injecta.vm10.com.br -filename injecta.bkp
#Restaurar backup de site
stsadm -o restore -url http://injecta.vm10.com.br -filename injecta.bkp -hostheaderwebapplicationurl http://sp01 -overwrite
 
# Desbloquear usuários
  use sharepoint_usr;
  select * from aspnet_membership order by islockedout desc;
  update aspnet_Membership set IsLockedOut = 0;
 
# Restaurar backup full
Instalar o WSS em outro servidor, tem que ser a mesma versão do WSS ou superior
Apagar a WebApplication padrão
Fazer o restore com o stsadm
Anexar a base ao banco
stsadm -o addcontentdb -url http://sp01 -databasename WSS_Content -databaseserver "SP03\Microsoft##SSEE"
 
# Para a pesquisa funcionar com hostheader e FBA (extender a webaplication para NTLM)
HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Lsa
DWORD - DisableLoopbackCheck = 1
 
# Select para verificar problemas na pesquisa
select * from MSSCrawlHostList
select * from MSSCrawlURLLog
select * from MSSCrawlHistory
select * from MSSCrawlQueue
select * from MSSCrawlErrorList
 
# Forçar uma nova indexação da pesquisa
C:\Program Files\Common Files\Microsoft Shared\Web Server Extensions\14\BIN>STSADM.EXE -o spsearch -action fullcrawlstart