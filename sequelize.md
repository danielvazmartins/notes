### Sequelize ###

# Instalar o sequelize-cli globalmente
npm install sequelize-cli -g

# Criar a estrutura inicial do sequelize no projeto
sequelize init

# Criar um model novo
sequelize model:generate --name customers --attributes cus_id:integer,cus_name:string,cus_status:boolean
sequelize model:generate --name users --attributes use_id:integer,use_email:string,use_name:string,use_nickname:string,use_password:string,use_admin:boolean
sequelize model:generate --name domains --attributes dom_id:integer,dom_url:string,dom_name:string
sequelize model:generate --name vpi_products --attributes vpr_id:integer,vpr_title:string,vpr_url:string,vpr_status:boolean
sequelize model:generate --name vpi_movies --attributes vmo_id:integer,vmo_url:string
sequelize model:generate --name tin_campaigns --attributes tca_id:integer,tca_name:string,tca_url:string
sequelize model:generate --name tin_likes --attributes tli_id:integer,tli_liked:boolean
sequelize model:generate --name tin_products --attributes tpr_id:integer,tpr_sku:string,tpr_title:string,tpr_url:string,tpr_image:string
Obs.: O arquivo de migrations é gerado adicionando um campo id como chave primária, ajustar o arquivo de migração e o models antes de rodar o migrate

# Sincronizar todos os arquivos de models com o banco de dados (criar tabelas no banco)
sequelize db:migrate

# Sincronizar apenas um arquivo específico
 sequelize db:migrate --to 20180629143627-create-users.js

# Desfazer a migração (remover tabelas do banco)
sequelize db:migrate:undo:all

# Desfazer a migração de um arquivo específico
sequelize db:migrate:undo --name 20180629134540-create-customers.js

# Criar um arquivo de seeder para alimentar o banco
sequelize seed:generate --name customers
sequelize seed:generate --name users
sequelize seed:generate --name domains
equelize seed:generate --name campaigns

# Popular o banco com os dados dos seeders
sequelize db:seed:all

# Popular o banco com os dados de um seeder específico
sequelize db:seed --seed 20180704142810-users.js

# Desfazer os seeders
sequelize db:seed:undo:all

# Desfazer o seeder de um arquivo
sequelize db:seed:undo --seed 20180704142810-users.js

https://www.learnacademy.org/current-days/569 verificar