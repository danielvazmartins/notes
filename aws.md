# Listar todas instancias
aws ec2 describe-instances
# Listar uma instancia
aws ec2 describe-instances --instance-ids i-5164d7b3
# Verificar zonas de disponibilidade
aws ec2 describe-availability-zones
# Pegar dados da instancia
wget -q -O - http://instance-data/latest/meta-data/
# Pegar o id da prÛpria instancia
wget -q -O - http://instance-data/latest/meta-data/instance-id