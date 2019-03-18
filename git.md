# Git

# Configurando nome e e-mail globalmente
# Obs.: É preciso configurar o email corretamente para aparecer nas contribuições do github
git config --global user.name "Daniel Vaz Villalobos Martins"
git config --global user.email "danielvazmartins@gmail.com"

# Configurar nome e e-mail por projeto
git config user.name "Daniel Vaz Villalobos Martins"
git config user.email "danielvazmartins@gmail.com"

# Baixar um projeto
git clone ssh://usuario@servidor:porta/path
git clone https://github.com/danielvazmartins/notes

# Verificar nome do server
git remote
git remote -v

# Commit
git add .
git commit
git push origin master

# Criar um novo repositório
git init --bare --shared=group nome-do-repositório
Ex.: git init --bare --shared=group avisos-ios

# Remover arquivo do servidor remoto
git rm --cached ARQUIVO
git rm -r --cached PASTA
git commit -a -m "A file was deleted"

# Configurando o git para o modo simples
git config --global push.default simple

# Ver todas branchs
git branch

# Criar uma branch nova
git branch novabranch

# Alterar a branch
git checkout novabranch

# Criar uma nova branch e já alterar para ela
git checkout -b novabranch2

# Jogando uma branch local no servidor
git push --set-upstream origin produto-api

# Atualizar estrutura de branchs
git fetch

# Ver todas as branch do servidor
git branch --remote

# Remover uma branch local
git branch -d nome-branch

# Remover uma branch remota
git push origin --delete nome-branch

# Ver status do projeto
git status

# Adicionar arquivos no stage/palco
git add arquivo

# Fazer commit das alterações do stage
git commit -m "Alteração do arquivo"

# Fazer o merge de uma branch para o master
git merge nomedabranch

# Voltar N posições de commit (rollback)
git revert -n HEAD~2..HEAD

# Desfazer as alterações locais
git reset --hard

# Voltar para um commit (testado para desfazer um commit que não subiu)
git reset --hard COMMITID

# Alterar um projeto existente para outro servidor
git remote -v
git remote remove origin
git remote add origin https://git.novoservidor.com.br/projetos/projeto-web
git branch --set-upstream-to=origin/master master
git push --set-upstream origin master

# Adicionar outro servidor remoto
git remote -v
git remote add backup https://user@bitbucket.org/user/remote.git
git push orign master
git push backup master