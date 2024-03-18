# 🔖 Git

## Configurações
```bash
# Configurando nome e e-mail globalmente
# Obs.: É preciso configurar o email corretamente para aparecer nas contribuições do github

git config --global user.name "Daniel Vaz Villalobos Martins"
git config --global user.email "danielvazmartins@gmail.com"

## Configurar nome e e-mail por projeto
git config user.name "Daniel Vaz Villalobos Martins"
git config user.email "danielvazmartins@gmail.com"

# Configurando o git para o modo simples
git config --global push.default simple
```

## Repositórios
```bash
# Baixar um projeto
git clone ssh://usuario@servidor:porta/path
git clone https://github.com/danielvazmartins/notes

# Verificar nome do servidor remoto
git remote
git remote -v

# Criar um novo repositório (local - working dir)
git init

# Criar um novo repositório (no servidor - shared)
git init --bare --shared=group nome-do-repositório
Ex.: git init --bare --shared=group avisos-ios

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
```

## Salvando alterações
```bash
# Salvando e subindo
git add .
git commit -m "comentarios"
git push origin [nome-da-branch]

# Ver todas branchs
git branch

# Criar uma branch nova
git branch novabranch

# Alterar para uma branch
git checkout novabranch

# Criar uma nova branch e já alterar para ela
git checkout -b novabranch2

# Renomear uma branch
gti branch -m oldbranch newbranch

# Vinculando a branch local com a remota
git branch --set-upstream-to=nome-da-branch-remote (Ex.: origin/master, origin/feature/branch)
git branch -u origin nome-da-branch

# Fazendo o push e vinculando a branch local com a remota
git push --set-upstream origin nome-branch
git push -u origin nome-branch

# Fazendo o push quando a branch remota já está vinculada
git push

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

# Altera a mensagem do último commit
git commit --amend -m "Nova mensagem do último commit"

# Fazer o merge de uma branch para a branch ativa
git merge nome-da-branch

# Unir commits
git rebase -i HEAD~N

# Fazer commit vazio
git commit --allow-empty -m "commit vazio"

# Visualizar o estado de algum commit
git checkout COMMITID

# Remover arquivo do servidor remoto
git rm --cached ARQUIVO
git rm -r --cached PASTA
git commit -a -m "A file was deleted"

# Copiando um commit de uma branch para outra
git cherry-pick COMMITID
```

## Stash - Trabalhando com arquivos ou alterações temporárias
```bash
# Salvando as alterações temporariamente (WIP)
git stash

# Salva as alterações na lista de stash especificando uma mensagem personalizada
git stash push -m "MESSAGE"

# Vendo lista de stash salvas
git stash list

// Traz de volta um stash salvo, se não especificar o stashId então retorna a última
git stash pop [stash] 

// Remove um stash da lista, se não especificar o stashId então remove o último
git stash drop [stash]
```

## Desfazendo alterações
```bash
# Removendo arquivos não trackeados
git clean -f

# Removendo arquivos e diretórios não trackeados
git clean -f -d

# Desfazer alterações em arquivos no working dir
git checkout arquivo
git checkout .
git restore arquivo
git restore .

# Voltando arquivo de staged para o working dir
git reset arquivo
git reset .
git reset HEAD arquivo

# Volta para um commit (cria um novo commit desfazendo a ação do anterior) e joga arquivos de commits posteriores no working dir (default)
# Não desfaz o commit remoto
git reset --mixed COMMITID
git reset COMMITID

# Desfaz N commits (cria uma commit para cada commit desfeito)
git reset HEAD~N

# Volta para um commit e joga arquivos de commits posteriores no stage
git reset --soft COMMITID

# Voltar para um commit e apaga os arquivos e alterações dos commits posteriores
git reset --hard COMMITID

# Desfaz todas alterações locais, de stage e do working dir
git reset --hard

# Git reset desfaz apenas os commits locais, se já tiver no servidor é preciso forçar o push
git push --force

# Desfazer alterações commitadas criando um novo commit (inclusive na branch remota)
git revert COMMITID
git revert HEAD

# Voltar N posições de commit (rollback)
? git revert -n HEAD~2..HEAD
``` 

## Ver alterações e logs
```bash
# Ver os logs (histórico de commits)
git log
git log --oneline
git log --decorate --oneline --graph --all
git log -p // Ver as modificações de cada commit
git log -p COMMIT ID // Ver as modificações de cada commit a partir do commit passado
git show COMMITID // Ver as modificações de um únido commit

# Para ver mais opções do 'git log'
https://devhints.io/git-log

# Ver alterações
git diff
git diff branch1..branch2 // Ver alterações entre duas branches
git diff COMMITHASH1..COMMITHASH2 //Ver todas diferenças de um commit até outro
```
