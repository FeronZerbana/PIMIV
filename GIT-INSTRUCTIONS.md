# Guia de Contribuição e Instruções Git para a Equipe

> Este documento estabelece o guia prático e obrigatório de versionamento Git para todos os desenvolvedores atuando nos subsistemas **Web**, **Desktop** e **Mobile** do projeto PIM IV.

---

## 1. Entendendo a Estrutura de Repositórios

O projeto utiliza o modelo de **Repositório Agregador com Git Submodules**:

```text
PIM/                     <- Repositório Pai (Orquestrador)
├── Documentacao/        <- Relatórios formais e acadêmicos do PIM
├── Implementacao/       <- [SUBMÓDULO] Código-fonte dos sistemas Web, Desktop e Mobile
└── Vault/               <- [SUBMÓDULO] Fonte Única da Verdade (SSOT: specs, regras, ADRs)
```

### Regra de Ouro de Navegação
* **Desenvolvimento de Código**: Todos os comandos de branch, commit e push de código-fonte devem ser executados **dentro da pasta `Implementacao/`**.
* **Documentação e Specs**: Todos os comandos de documentação devem ser executados **dentro da pasta `Vault/`**.
* **Repositório Pai**: A pasta raiz `PIM/` serve apenas para gerenciar os apontamentos dos submódulos e documentação geral.

---

## 2. Como Clonar e Configurar o Ambiente de Trabalho

### 2.1. Clonagem Inicial Completa
Para baixar o repositório pai e todos os submódulos de uma única vez:

```bash
git clone --recurse-submodules https://github.com/FeronZerbana/PIMIV.git
cd PIM
```

### 2.2. Para Quem Já Clonou sem Submódulos
Se você já clonou apenas o repositório pai e as pastas `Implementacao` e `Vault` vieram vazias:

```bash
cd PIM
git submodule update --init --recursive
```

---

## 3. Modelo de Branches e Atribuição de Responsabilidades

O repositório de `Implementacao` conta com as seguintes branches principais:

| Branch | Responsabilidade | Equipe Envolvida |
| :--- | :--- | :--- |
| `production` | Versão final consolidada, estável e integrada | Líder Técnico / Release Manager |
| `develop` | Branch de integração contínua entre Web, Desktop e Mobile | Todos os desenvolvedores |
| `feat/web` | Branch base de funcionalidades do Sistema Web (ASP.NET Core MVC) | Desenvolvedores Web |
| `feat/desktop` | Branch base de funcionalidades do Sistema Desktop (PDV / Hardware) | Desenvolvedores Desktop |
| `feat/mobile` | Branch base de funcionalidades do Sistema Mobile | Desenvolvedores Mobile |

---

## 4. Como Trabalhar em sua Plataforma (Passo a Passo)

### 4.1. Entrar na pasta do submódulo
Antes de qualquer comando Git de código, entre no diretório `Implementacao`:

```bash
cd c:/Users/vinic/Documents/PIM/Implementacao
```

### 4.2. Evitar o Estado de Detached HEAD
Ao clonar submódulos, o Git pode deixá-lo em um commit solto (`detached HEAD`). Certifique-se sempre de apontar para a branch de trabalho da sua equipe:

* **Se você trabalha no Web**:
  ```bash
  git checkout feat/web
  git pull origin feat/web
  ```
* **Se você trabalha no Desktop**:
  ```bash
  git checkout feat/desktop
  git pull origin feat/desktop
  ```
* **Se você trabalha no Mobile**:
  ```bash
  git checkout feat/mobile
  git pull origin feat/mobile
  ```

### 4.3. Criação de Novas Branches de Feature
Para desenvolver uma funcionalidade específica, crie uma sub-branch a partir da branch base da sua plataforma, seguindo o padrão de nomenclatura:

* **Padrão de Nomenclatura**:
  * `feat/web/<identificador-ou-nome-da-tarefa>`
  * `feat/desktop/<identificador-ou-nome-da-tarefa>`
  * `feat/mobile/<identificador-ou-nome-da-tarefa>`
  * `fix/web/<nome-do-bug>` (para correções)

* **Exemplo Prático (Desenvolvedor Web criando tela de Login)**:
  ```bash
  # 1. Garanta que está na branch base da plataforma atualizada
  git checkout feat/web
  git pull origin feat/web

  # 2. Crie sua branch de trabalho
  git checkout -b feat/web/autenticacao-login
  ```

* **Exemplo Prático (Desenvolvedor Desktop criando integração com impressora)**:
  ```bash
  git checkout feat/desktop
  git pull origin feat/desktop
  git checkout -b feat/desktop/driver-impressora-termica
  ```

---

## 5. Padrão de Commits

### 5.1. Verificação Pré-Commit
Antes de adicionar arquivos para commit, confirme onde você está:

```bash
git status
git branch
```
Verifique se a branch ativa é de fato a sua branch de trabalho (`feat/web/...`, etc.) e não `production` ou `master`.

### 5.2. Padrão de Mensagens (Sem Emojis e em Português)
Adotamos o padrão Conventional Commits em português, estritamente **sem emojis**:

* `feat: <descrição>` - Nova funcionalidade baseada em spec.
* `fix: <descrição>` - Correção de defeito/bug.
* `refactor: <descrição>` - Refatoração interna sem alteração de comportamento externo.
* `test: <descrição>` - Adição ou ajuste de testes automatizados.
* `chore: <descrição>` - Alterações de configuração, dependências ou infraestrutura.
* `docs: <descrição>` - Alterações exclusivamente documentais.

### 5.3. Exemplo Prático de Commit
```bash
git add WEB/Controllers/AccountController.cs WEB/Views/Account/Login.cshtml
git commit -m "feat(web): implementacao do formulario de login e validacao de credenciais"
```

---

## 6. Como Fazer Push para o Repositório Remoto

### 6.1. Primeiro Push da sua Nova Branch
Ao subir uma branch nova que ainda não existe no GitHub, configure o rastreamento upstream:

```bash
git push -u origin feat/web/autenticacao-login
```

### 6.2. Pushes Subsequentes
Após o upstream estar configurado, basta executar:

```bash
git push origin feat/web/autenticacao-login
```

---

## 7. Perigos Críticos e Cuidados Necessários

### 7.1. Perigo 1: Comitar Código na Raiz `PIM/` em vez de `Implementacao/`
* **O Problema**: Se você executar `git commit` na pasta raiz `PIM/`, você estará apenas salvando o ponteiro de versão do submódulo, e não o código-fonte em si.
* **A Prevenção**: Sempre verifique o diretório atual no terminal antes de comitar. O código-fonte dos sistemas reside exclusivamente dentro de `PIM/Implementacao/`.

### 7.2. Perigo 2: Uso Destrutivo de `git push --force`
* **O Problema**: Executar `git push --force` ou `git push -f` em branches compartilhadas (`develop`, `production`, `feat/web`, `feat/desktop`, `feat/mobile`) pode apagar commits enviados por outros colegas de equipe.
* **A Prevenção**:
  * É **proibido** o uso de `--force` em branches principais.
  * Em branches pessoais de feature, caso tenha feito um rebase local, utilize exclusivamente `--force-with-lease` para garantir que ninguém mais subiu alterações na mesma branch:
    ```bash
    git push --force-with-lease origin feat/web/minha-feature
    ```

### 7.3. Perigo 3: Subir Código Sem Spec no Vault
* **O Problema**: O projeto opera sob a regra de ouro **Proibido Código Sem Spec**.
* **A Prevenção**: Antes de iniciar o desenvolvimento, valide se a especificação técnica está aprovada em `Vault/04-Specs-Backlog/Active/`.

### 7.4. Perigo 4: Conflitos por Falta de Atualização Frequente
* **O Problema**: Ficar dias desenvolvendo sem sincronizar sua branch com as alterações mais recentes da equipe.
* **A Prevenção**: Diariamente, integre as novidades da branch base na sua branch de feature:
  ```bash
  git checkout feat/web
  git pull origin feat/web
  git checkout feat/web/minha-feature
  git merge feat/web
  ```

---

## 8. Como Atualizar o Repositório Agregador (PIM)

Após comitar e enviar suas alterações dentro de `Implementacao/` ou `Vault/`, caso seja necessário atualizar o repositório agregador para fixar as novas versões dos submódulos:

```bash
# 1. Vá para a raiz do repositório pai
cd c:/Users/vinic/Documents/PIM

# 2. Verifique que o Git detectou novos commits nos submódulos
git status

# 3. Adicione as atualizações dos submódulos e faça o commit
git add Implementacao Vault
git commit -m "chore: atualizacao dos ponteiros dos submodulos Implementacao e Vault"

# 4. Envie para o repositorio pai
git push origin master
```

---

## 9. Guia de Resolução de Problemas Comuns (Troubleshooting)

### Cenário A: Entrei em estado de `detached HEAD` no submódulo
```bash
# Verifique em que commit você está
git log -1 --oneline

# Mude para a branch correta da sua equipe
git checkout feat/web   # ou feat/desktop / feat/mobile

# Atualize a branch
git pull origin feat/web
```

### Cenário B: Comitei na branch errada localmente (antes de fazer push)
```bash
# 1. Desfaça o último commit mantendo suas alterações nos arquivos
git reset --soft HEAD~1

# 2. Crie e mude para a branch correta
git checkout -b feat/web/nome-correto

# 3. Refaça o commit na branch correta
git add .
git commit -m "feat(web): descricao da feature"
```

### Cenário C: Meu colega subiu uma alteração no submódulo e minha pasta não atualizou
```bash
# Na raiz do repositório pai
cd c:/Users/vinic/Documents/PIM
git pull origin master
git submodule update --recursive
```
