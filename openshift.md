### OpenShift ###

# Fazer o download do client
https://www.okd.io/download.html
https://blog.openshift.com/installing-oc-tools-windows/

```bash
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

# Copiar arquivo do pod para a máquina
oc rsync POD:/PATH PATH_LOCAL

# Sincronizar diretório da máquina local para o pod
oc rsync PATH_LOCAL POD:/PATH

# Desconectar
oc logout
```