### OpenShift ###

# Fazer o download do client
https://www.okd.io/download.html
https://blog.openshift.com/installing-oc-tools-windows/

# Conectar no OpenShift
oc login https://url-console-openshift:8443

# Verificar todos projetos
oc get projects

# Alterar o projeto
oc project NOME-PROJETO

# Listar os PODs do projeto
oc get pods

# Conectar via SSH usando o client
oc rsh NOME-DO-POD

# Copiar arquivo do pod para a maquina local
oc rsync origem destino

# Desconectar
oc logout