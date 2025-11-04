# 🚀 Onboarding do Time — Git & GitHub (Fluxo por Branch)

Este guia explica como **cada integrante** deve configurar o ambiente local, sincronizar o código com o repositório remoto e enviar atualizações **somente para sua própria branch**, mantendo a `main` estável e sem riscos de conflito.

---

## ⚙️ Configuração Inicial (Primeira Vez)

### 🔹 Verifique se o Git está instalado
```bash
git --version
```
### 🔹 Configure suas credenciais (obrigatório para commits)
```bash
git config --global user.name "Seu Nome Sobrenome"
git config --global user.email "seuemail@exemplo.com"
```
### 🔹 Ajuste de boas práticas no push/pull
```bash
git config --global push.default current
git config --global pull.rebase true
```
## 🧩 Clonando o Repositório
Clone o repositório do projeto:
```bash
git clone https://github.com/devpedrois/PROJETO-PIF.git
cd PROJETO-
```
Liste e atualize todas as branches remotas:
```bash
git fetch --all --prune
git branch -a
```
Crie e ative sua branch local rastreando a branch remota:
```bash
# Exemplo para a branch "gabriel"
git switch -c gabriel --track origin/gabriel
# ou:
git checkout -b gabriel origin/gabriel
```
Confirme onde você está:
```bash
git status
# deve mostrar: On branch gabriel (ou sua branch)
```

## 🧠 Rotina Diária Antes de Começar a Codar

### 🔸 Atualize a branch main (base do projeto)
```bash
git switch main
git pull origin main
```

### 🔸 Volte para a sua branch e traga as novidades da main:
```bash
git switch <sua-branch>
```
Opção A — Merge (mais simples)
```bash
git merge origin/main
```
Se houver conflitos: resolva no VS Code (Accept Current/Incoming/Both), depois:
```bash
git add .
git commit -m "merge: atualiza <sua-branch> com origin/main"
```
Opção B — Rebase (mantém histórico limpo)
```bash
git rebase origin/main
# se houver conflitos:
git add .
git rebase --continue
```
⚠️ Regra de Ouro: nunca faça commits diretamente na main.
Trabalhe apenas na sua branch.

## 💾 Salvando e Enviando Alterações
Após editar o código:
```bash
# verifique mudanças
git status

# adicione arquivos modificados
git add .

# crie um commit com mensagem clara
git commit -m "feat: adiciona lógica da tabela verdade"
```

Envie apenas para sua branch:
```bash
git push -u origin <sua-branch>
# nas próximas vezes, apenas:
git push
```

Se o push for rejeitado:
```bash
git pull --rebase
# resolva conflitos -> add -> rebase --continue
git push
```
## 🔄 Sincronizando com a Main (Regularmente)
Mantenha sua branch atualizada com a versão mais recente da main:
```bash
git switch main
git pull origin main

git switch <sua-branch>
git merge origin/main
# ou:
git rebase origin/main
```

## 🧾 Enviando Alterações para Revisão (Pull Request)
Quando finalizar uma tarefa:
1️⃣ Envie suas alterações:
```bash
git push
```
2️⃣ No GitHub, abra um Pull Request de:
```bash
<sua-branch> → main
```

3️⃣ Peça revisão de código a um colega.
4️⃣ Nunca faça merge direto na main sem aprovação.

## 🔁 Atualizando o Projeto ao Voltar a Trabalhar
```bash
# 1) atualize a main
git switch main
git pull origin main

# 2) volte para sua branch e sincronize
git switch <sua-branch>
git merge origin/main   # ou git rebase origin/main

# 3) trabalhe normalmente
git add .
git commit -m "fix: corrige detecção de colisão"
git push
```

## 💡 Boas Práticas
```bash
✅ Commits pequenos e mensagens padronizadas (feat:, fix:, chore:, docs:)
✅ Sempre puxe antes de começar a programar
✅ Teste localmente antes de enviar
✅ Faça PRs curtos e frequentes
✅ Evite renomear branches sem comunicar
✅ Nunca envie arquivos compilados — mantenha o .gitignore atualizado
```

🧠 Dica: Sempre confira sua branch ativa com git status antes de dar add, commit ou push.
Um comando errado pode afetar o projeto de todo o time.
