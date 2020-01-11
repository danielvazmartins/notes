### MySQL ###

#Acessar banco via client
mysql -h HOST -D DATABASE -u USER -p

#Visualizar queries rodando
show processlist
show processlist\G
show full processlist

 
#Adicionar coluna
alter table filtros add column acctWebmail char(1) default "Y";
 
#Adicionar coluna com auto incremento
alter table emaillog add column logid bigint AUTO_INCREMENT KEY;
 
#Configurar o valor do auto incremento
ALTER TABLE tablename AUTO_INCREMENT = 1
 
#Alterar uma coluna
alter table accounts modify acctQtdEmailsHour int(10) default 1000;
 
# Verificar os indices de uma tabela
show index from devices_test;
# Remover um index
alter table devices_test drop index dev_unique;
# Criar um index
create unique index dev_unique on devices_test (clicod,appcod,`desc`);
 
#Criar tabela nova
CREATE TABLE dailylog (
  `logid` bigint(20) NOT NULL auto_increment,
  `logdate` date default NULL,
  `domainID` int(11) default NULL,
  `resellerID` int(11) default NULL,
  `logQtdeEnv` int(11) default NULL,
  `logQtdeRec` int(11) default NULL,
  `logBytesEnv` bigint(20) default NULL,
  `logBytesRec` bigint(20) default NULL,
  PRIMARY KEY  (`logid`)
)
 
#Criar usuário para acessar o banco (Fazer para o localhost e para o IP e % se precisar)
grant all on ispvm.* to suporte@'localhost' identified by "teste10";
flush privileges;
OU
create user isp@'localhost' identified by "q1Q!q1Q!";
grant all on ispvm.* to isp@'localhost';
flush privileges;
# Visualisar os usuários do banco
select * from mysql.user;
select Host, User from mysql.user;
 
# Exportar apenas o conteudo de uma tabela
mysqldump pushec --skip-add-drop-table --no-create-info --tables apps -p > pushec.bkp
 
#Visualizar lista de anexos
select domainID, acctEmail, acctAttachControl, acctAttachList from accounts where domainID in (44,45,46);
#Atualizar lista de anexos da rolamentosradial
update accounts set acctAttachList = 'eml,txt,xls,doc,jpeg,pdf,ods,dwg,jpg,png,gif,bmp,tif,htm,html,rtf,xlsx,docx,vcf,dat,odt,dot,dwf,mso,xml,wmz,mdi,wmf,emz' where domainID in (44,45,46);
#Obs.: Adicionar a extensão zip nas contas
update accounts set acctAttachList = 'eml,txt,xls,doc,jpeg,pdf,ods,dwg,jpg,png,gif,bmp,tif,htm,html,rtf,xlsx,docx,vcf,dat,odt,dot,dwf,mso,xml,wmz,mdi,wmf,emz,zip' where domainID in (44,45,46) and acctEmail = 'alessandra@rolamentosradial.com.br';
alessandra@rolamentosradial.com.br
vantuir@rolamentosradial.com.br
ahmad@rolamentosradial.com.br
 
update accounts set acctAttachList = CONCAT("eml,",acctAttachList) where domainID in (44,45,46);
 
#Atualizar filtro de anexos da emefarmario.com.br
update accounts set acctAttachControl = "Y", acctAttachList = "doc,txt,xls,jpg,jpeg,xlsx,docx,rar,zip,xml,html,pdf,gif,ods,bmp,eml,tif,png,odt,xps" where domainID = 177 and acctType="C" and planID = 13;
select domainID, acctEmail, acctAttachControl, acctAttachList from accounts where domainID = 177;
 
#Atualizar filtro de anexos da agabe.com
update accounts set acctAttachList = "odp,odt,xps,ods,std,dwg,dot,doc,docx,xls,xlsx,txt,jpg,bmp,gif,png,cdr,xml,htm,html,qxp,ai,pdf,jpeg,psd,tif,eps,dot,dotx,rtf,zip,rar,dat,7zip" where domainID = 410 and acctType="C" and acctAttachControl = "Y";
select domainID, acctEmail, acctAttachControl, acctAttachList from accounts where domainID = 410;
 
#Desativar antispam
update accounts set acctBypassSpam = 'Y' where domainID in (44,45,46);
 
#Tamanhos das caixas de email por grupo
select deptDesc AS Grupo, ROUND(SUM(acctQuotaUsed)/1000/1000/1000,2) AS "Tamanho(GB)", ROUND(SUM(acctQuotaUsed)*100/119826358235,2) AS "%" from accounts a inner join departments d on a.deptID = d.deptID where a.domainID = 60 group by a.deptID order by deptDesc;
 
#Gerar CSV para o microsoft transportar (Domínio pcinformatica)
select CONCAT(acctEmail,',10.14.78.132,',acctEmail,',',acctPassword,',',acctUsername,'@pcinformatica.vm10.com.br') AS CSV from accounts where domainID = 60 and acctType ='C' and planID = 11 INTO OUTFILE '/tmp/pcinformatica';
#Listas
select CONCAT(SPLIT_STR(acctEmail,"@",1),",",listDisplayName) from accounts where acctType = "L" and domainID = 60 INTO OUTFILE"/tmp/lists";
#Membros das listas
select CONCAT(SPLIT_STR(acctEmail,"@",1),",",listMemberEmail) from listsMembers where domainID = 60 INTO OUTFILE"/tmp/members";
 
#Atualizar o acctTransport das listas e apelidos com os transportes do domínio
update accounts a set acctTransport = (select domainTransport from domainPlat b where b.domainID = a.domainID and platCod = a.acctPlatform) where acctType in ("A","L") order by acctPlatform;
 
#Criar apelidos zimbra para todas contas de determinado domínio
insert into accounts select 681, 1, concat(acctUsername,"@swagelokbrasil.net.br"), NULL, NULL,"","",1,0,"","A",0,0,0,"",200,"","","","","",acctEmail,0,NULL,0,"",0,1,"",0,0,0,"local","N",NULL,"N",300,"N","N","U","N","N","Y",NULL,NULL,0,0,100,0,1,NULL from accounts where domainID = 678;
 
#Criar apelidos exchange para todas contas de determinado domínio
insert into accounts select 852,1,concat(acctUsername,"@bmbmodecenter.com.br"),NULL,NULL,"","",1,0,"","A",0,0,0,"",200,"","","","","",acctEmail,0,NULL,0,"MBX03DB2",0,4,"smtp:ex-int.vm10.com.br:25",0,0,0,"local","N",NULL,"N",300,"N","N","U","N","N","Y",NULL,NULL,0,0,100,0,1,NULL,NULL,"Y" from accounts where domainID = 851;
 
#Número de contas contratadas por servidor
select domainServer, SUM(domainPlanQtdAccount), SUM(domainPlanSpace) from domains a inner join domainPlat b on a.domainID = b.domainID inner join domainPlan c on a.domainID = c.domainID and b.platCod = c.platID group by domainServer;
 
#Gerar lista dos e-mails em formato csv
select concat(coalesce(acctFName,""),coalesce(acctMName,""),coalesce(acctLName,""),",",acctEmail) from accounts where domainID = 844 and acctType = "C"