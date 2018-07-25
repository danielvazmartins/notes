#Comandos Exchange

#Configurar tempo limite de email na fila
Set-TransportServer -Identity EDC -MessageExpirationTimeout 06:00:00
#Pegar informações da MailBox
Get-MailboxStatistics -Identity andre@printsys.com.br
#Dar permissão na MailBox para o Administrador
Add-MailboxPermission -Identity andre@printsys.com.br -User administrator -AccessRights FullAccess
#Gerar PST
Export-Mailbox -Identity andre@printsys.com.br -PSTFolderPath e:\andre.pst
#Gerar PST e apagar conteudo da MailBox
Export-Mailbox -Identity andre@printsys.com.br -PSTFolderPath e:\andre2.pst -DeleteAssociatedMessages -DeleteContent
#Importar PST
Import-Mailbox -Identity andre@printsys.com.br -PSTFolderPath e:\andre2.pst
#Importar PST a partir da certa data
Import-Mailbox -Identity andre@printsys.com.br -PSTFolderPath e:\andre2.pst -StartDate 30/5/2009
#Aplica MailBox Policy em um usuário
Set-Mailbox -Identity daniel.martins@viewit.com.br -ManagedFolderMailboxPolicy "Apagar mensagens antigas"
#Executar MailBox Policies
Start-ManagedFolderAssistant
#Gerar Requisição de Certificado
New-ExchangeCertificate -DomainName exchange02.vm10.com.br -GenerateRequest:$true -KeySize 1024 -Path d:\exchange02.req -PrivateKeyExportable:$true -SubjectName "OU=Domain Control Validated, CN=exchange02.vm10.com.br, O=exchange02.vmm10.com.br"
 
#Pegar o ID do usuário do Recovery Storage Group
Get-MailboxStatistics -Database W04\RSG\DB2 |sort DisplayName |ft DisplayName, Identity
#Restaurar backup da Recovery Storage Group para uma caixa de email diferente
Restore-Mailbox -Identity "EMAIL-DE-DESTINO" -RSGDatabase "DATABASE-DO-RSG" -RSGMailbox GUID-DA-CONTA-DO-RSG
Restore-Mailbox -Identity daniel25dif@viewit.com.br -RSGDatabase "W03\Recovery Storage Group\DB1" -RSGMailbox d43325e7-9d7a-4396-8c86-67579883797d
#Gerar arquivo CSV com as contas de e-mail ordenadas por nome
Get-Mailbox |Select Name,Alias |sort Name |ConvertTo-CSV |Out-File d:\temp\usuarios.txt
#Gerar arquivo CSV com as contas de e-mail e espaço utilizado por cada uma
Get-Mailbox |Get-MailboxStatistics |select DisplayName,TotalItemSize |sort TotalItemSize |ConvertTo-CSV |Out-File d:\temp\tamanho.txt
#Gerar arquivo CSV com as contas de e-mail de determinada Database e espaço utilizado por cada uma
Get-Mailbox |where {$_.Database -eq "Mailbox Database 500MB"} |Get-MailboxStatistics |select DisplayName,TotalItemSize |sort TotalItemSize |ConvertTo-CSV |Out-File d:\temp\tamanho.txt
#Contas de determinada Database maiores que certo tamanho
Get-Mailbox |where {$_.Database -eq "Mailbox Database 500MB"} |Get-MailboxStatistics |where {$_.TotalItemSize -ge 500000000}|select DisplayName,TotalItemSize |sort TotalItemSize
# Pegar total de contas, tamanho total, minumo, máximo e média das mailboxes
Get-Mailbox |Get-MailboxStatistics | %{$_.TotalItemSize.Value.ToMB()}| measure -Sum -Maximum -Minimum -Average
# Pegar o tamanho total utilizado por um domínio
Get-Mailbox |? {$_.CustomAttribute1 -eq "porte-com-br"} |Get-MailboxStatistics |%{$_.TotalItemSize.Value.ToMB()} |Measure-Object -Sum
 
# Limites para envio de mala direta
Set-ReceicerConnector nome -MaxAcknowledgement 0
Set-ReceicerConnector nome -TarpitInterval 0
Add-AdPermission -Identity "nome receiver connector" -User "NT AUTHORITY\Authenticated Users" -ExtendedRights ms-Exch-SMTP-Accept-Any-Sender
 
Set-ReceiveConnector -Identity "PC-EXCHANGE\Client PC-EXCHANGE" -MessageRateLimit 100
 
# Gerar csv com contas que tem encaminhamento
Get-Mailbox -ResultSize Unlimited |select UserPrincipalName, ForwardingAddress |where {$_.ForwardingAddress -like "*v*"} |Export-Csv d:\forward.txt