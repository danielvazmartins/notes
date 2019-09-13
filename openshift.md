# OpenShift Client

```bash
# Conectar
oc login https://console.paas.santanderbr.pre.corp:8443

# Listar projetos
oc projects

# Trocar de projeto
oc project PROJETO

# Listar todos pods do projeto
oc get pods

# Conectar via SSH no pod
oc rsh POD

# Copiar arquivo do pod para a máquina
oc rsync POD:/PATH PATH_LOCAL

# Sincronizar diretório da máquina local para o pod
oc rsync PATH_LOCAL POD:/PATH
```