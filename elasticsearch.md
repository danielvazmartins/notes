# Elasticsearch

# Iniciar no Windows habilitando CORS para qualquer origem
elasticsearch.exe -E http.cors.enabled=true -E http.cors.allow-origin="*" 

# Acessar o kopf
http://localhost:9200/_plugin/kopf/#!/rest

# Comandos para verificar informações e status do servidor
http://localhost:9200/
http://localhost:9200/_cat/health?v
http://localhost:9200/_cat/indices?v
http://localhost:9200/_cat/nodes?v

# Pesquisar (tudo)
_search

# Pesquisar database
/index/_search (Ex.: /push/_search)

# Pesquisar tabela
/index/type/_search (Ex.: /push/lojas/_search)

# Filtrar pelo valor de um campo
curl -XPOST 'http://localhost:9200/push/logs/_search' -d '{
  "query": {
    "match": {
      "deptoId": "44"
    }
  },
  "size": 3
}'

# Pesquisar por um campo faltando ou null
curl -XPOST 'http://localhost:9200/push/logs/_search' -d '{
  "filter": {
    "missing": {
      "field": "deptoId"
    }
  },
  "size": 3
}'

# Retornar um campo pelo id
curl -XGET 'http://localhost:9200/push/logs/AVkIyNdgbAgWLbOUn5mQ'

# Remover um campo pelo id
curl -XDELETE 'http://localhost:9200/push/logs/AVkIyNdgbAgWLbOUn5mQ'

# Criar um repositorio para backup
PUT _snapshot/elastic_backup
{
  "type": "s3",
  "settings": {
    "bucket": "viewit-elasticsearch",
    "region": "sa-east-1"
  }
}

# Ver todos repositorios
GET _snapshot/

# Criar um snapshot
PUT /_snapshot/elastic_backup/snapshot_1?wait_for_completion=true

# Ver todos snapshots do repositorio
GET _snapshot/elastic_backup/_all

# Fazendo um restore, alterando o nome do indice
POST /_snapshot/elastic_backup/snapshot_1/_restore?wait_for_completion=true
{
  "indices": "push_112016",
  "rename_pattern": "push_(.+)",
  "rename_replacement": "restored_push_$1"
}

## Links Uteis

# Logstash com docker
https://www.elastic.co/guide/en/logstash/current/docker-config.html

# Elasticsearch com docker
https://www.elastic.co/guide/en/elasticsearch/reference/current/docker.html

# Logstash output plugins
https://www.elastic.co/guide/en/logstash/current/output-plugins.html

# API em Javascript Node para o elasticsearch
https://www.elastic.co/guide/en/elasticsearch/client/javascript-api/current/about.html

# Agrupando dados com o elasticsearch
https://m.alphasights.com/practical-guide-to-grouping-results-with-elasticsearch-a7e544343d53