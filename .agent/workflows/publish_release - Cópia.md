---
description: Como publicar uma nova release do ManagerX (Template Genérico)
---

# Fluxo de Publicação de Release

Este guia descreve os passos genéricos para arquivar a versão anterior e publicar uma nova versão no repositório GitHub.

## Variáveis

Antes de começar, identifique os valores:

- `<V_ANT>`: Versão que está atualmente como `ManagerX.pcz` (ex: `1.3.5`)
- `<V_NOVA>`: Nova versão que pretende publicar (ex: `1.3.6`)

## Passos

### 1. Preparar os Ficheiros na Raiz

Mova a versão atual para o histórico e prepare a nova versão principal:

```powershell
# 1. Mover a versão atual para a pasta de histórico com o número de versão correto
mv ManagerX.pcz "old_releases/ManagerX<V_ANT>.pcz"

# 2. Renomear o seu novo ficheiro (que deve estar na raiz) para ser o principal
mv "ManagerX<V_NOVA>.pcz" ManagerX.pcz
```

### 2. Sincronizar com Git

Registe as alterações no histórico do Git:

```powershell
# Adicionar as alterações (a remoção/renomeação e o novo ficheiro)
git add .

# Criar o commit da release
git commit -m "Release v<V_NOVA>"

# Enviar para o GitHub
git push origin main
```

### 3. Criar Tag e Release no GitHub

Crie a tag de versão para marcar este ponto no código e publique a entrada oficial:

```powershell
# Criar e enviar a tag (sempre com o prefixo 'v')
git tag "v<V_NOVA>"
git push origin "v<V_NOVA>"

# Criar a Release no GitHub anexando o ficheiro principal
gh release create "v<V_NOVA>" ManagerX.pcz --title "ManagerX v<V_NOVA>" --notes "Release v<V_NOVA>"
```

## Resumo da Estrutura Resultante

- `ManagerX.pcz`: Sempre a versão mais recente disponível para download automático.
- `old_releases/`: Contém todos os ficheiros das versões passadas para histórico.
- **GitHub**: Uma nova entrada na página "Releases" com o ficheiro atualizado.
