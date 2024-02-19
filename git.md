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
``````

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
git commit
git push origin master

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

# Jogando uma branch local no servidor
git push --set-upstream origin nome-branch
git push -u origin nome-branch

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

# Fazer o merge de uma branch para a branch ativa
git merge nomedabranch

# Unir commits
git rebase -i HEAD~N

# Fazer commit vazio
git commit --allow-empty -m "commit vazio"

# Salvando as alterações temporariamente
git stash
git stash list
git pop //Traz de volta as alterações salvas

# Visualizar o estado de algum commit
git checkout COMMITID

# Remover arquivo do servidor remoto
git rm --cached ARQUIVO
git rm -r --cached PASTA
git commit -a -m "A file was deleted"
```

## Desfazendo alterações
```bash
# Desfazer alterações que não foram adicionadas ao stage
git checkout -- arquivo

# Desfazer alterações no stage mas não comitadas
git reset HEAD arquivo

# Volta para um commit e joga arquivos de commits posteriores no stage
git reset --soft COMMITID

# Volta para um commit e joga arquivos de commits posteriores no working dir
git reset --mixed COMMITID

# Desfazer as alterações locais
git reset --hard

# Voltar para um commit e apaga commits posteriores
git reset --hard COMMITID

# Desfazer alterações commitadas
git revert COMMITID

# Voltar N posições de commit (rollback)
git revert -n HEAD~2..HEAD
``` 

## Ver alterações e logs
```bash
# Ver os logs (histórico de commits)
git log
git log --oneline
git log -p // Ver as modificações de cada commit

# Para ver mais opções do 'git log'
https://devhints.io/git-log

# Ver alterações
git diff
git diff branch1..branch2 // Ver alterações entre duas branches
git diff COMMITHASH1..COMMITHASH2 //Ver todas diferenças de um commit até outro
```
