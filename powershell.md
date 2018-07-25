#omandos PowerShell

#Combinando a saida de dois comandos com o select
[PS] C:\>Get-Mailbox daniel.martins@viewit.com.br | select PrimarySmtpAddress, @{n="Status"; e={Get-MailboxStatistics $_.name |select StorageLimitStatus}}
 
 
[PS] C:\>Get-Mailbox -Database w03\sg1\db1 | Where{$_.CustomAttribute1 -eq "deltadecisao-com-br"}| select PrimarySmtpAddress, @{n="Status"; e={Get-MailboxStatistics $_.name |select TotalItemSize}} |sort TotalItemSite
 
# Gera lista de usuários com e-mails na caixa de saída
Get-Mailbox | Get-MailboxFolderStatistics -FolderScope Outbox |select Identity, FolderSize |sort FolderSize |Export-Csv -NoTypeInformation -Path c:\outbox.txt