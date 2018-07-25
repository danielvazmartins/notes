#Comandos Exchange 2010

#Exportar PST
New-MailboxExportRequest -Mailbox daniel.martins@viewit.com.br -FilePath \\ex01\d$\temp\2010\daniel.pst
#Verificar andamento da exportação
Get-MailboxExportRequest |Get-MailboxExportRequestStatistics
#Remove requisições de exportação
Get-MailboxExportRequest |Remove-MailboxExportRequest
#Importar PST
New-MailboxImportRequest -Mailbox import@viewit.com.br -FilePath '<\\ex01\d$\temp\2010\daniel.pst'  -BadItemLimit 10 -ExcludeDumpster>
#Verificar andamento da importação
Get-MailboxImportRequest |Get-MailboxImportRequestStatistics
#Remove requisições de importação
Get-MailboxImportRequest |Remove-MailboxImportRequest
 
#Enviar email via PowerShell
Send-MailMessage -To daniel.martins@viewit.com.br -Subject teste -From daniel.martins@viewit.com.br -SmtpServer 10.14.78.142
 
#Adicionar permissões para o besadmin para novas bases
Get-MailboxDatabase |Add-ADPermission -User besadmin -AccessRights ExtendedRight -ExtendedRights Receive-As, ms-Exch-Store-Admin
#Verificar as permissões do besadmin nas bases
Get-MailboxDatabase |Get-ADPermission -User besadmin
 
New-MailboxDatabase -Name RSG -Recovery -EdbFilePath Z:\RSG\rsg.edb -Server mbx01
 
# Configurações de Antispam (almenat - emails com SPAM no assunto caia na caixa de entrada)
Get-Mailbox -ResultSize unlimited |? {$_.CustomAttribute1 -eq "almenat-com-br"} |Set-Mailbox -SCLJunkThreshold 8 -SCLJunkEnabled $true
Get-Mailbox -ResultSize unlimited |? {$_.CustomAttribute1 -eq "almenat-com-br"} |ft Name, SCLJunkThreshold, SCLJunkEnabled
 