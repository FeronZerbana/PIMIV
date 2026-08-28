# Projeto Integrado Multidisciplinar (PIM IV)

> Repositório agregador e orquestrador do projeto PIM IV, conectando a governança documental e a implementação dos sistemas Web, Desktop e Mobile através de submódulos Git.

---

## 1. Estrutura do Ecossistema

```text
PIM/
├── .gitmodules             # Definição e mapeamento dos submódulos remotos
├── GIT-INSTRUCTIONS.md     # Guia completo de versionamento Git e fluxo de branches
├── Documentacao/           # Relatórios acadêmicos, diagramas e entregáveis formais do PIM
├── Implementacao/          # [Submódulo Git] Código-fonte (Web, Desktop, Mobile)
│   ├── WEB/                # Sistema Web em ASP.NET Core MVC
│   ├── DESKTOP/            # Sistema Desktop / PDV / Frente de Caixa
│   └── MOBILE/             # Sistema Mobile
└── Vault/                  # [Submódulo Git] Fonte Única da Verdade (SSOT)
    ├── 00-Meta/            # Governança, Políticas e Modelos (Specs/ADRs)
    ├── 01-Core-Domain/     # Regras de Negócio Universais & Contratos de API
    ├── 02-Legacy-Analysis/ # Mapeamento e débitos do sistema legado
    ├── 03-Systems/         # Especificações técnicas particionadas por cliente
    ├── 04-Specs-Backlog/   # Pipeline de aprovação de features (Draft -> Active -> Completed)
    └── 05-Architecture-Knowledge/ # ADRs e Pesquisas Técnicas
```

---

## 2. Como Clonar e Inicializar o Projeto

Para clonar o projeto completo com todos os submódulos populados:

```bash
git clone --recurse-submodules https://github.com/FeronZerbana/PIMIV.git
cd PIM
```

Se você já clonou sem o parâmetro de submódulos, inicialize-os com:

```bash
git submodule update --init --recursive
```

---

## 3. Guia Rápido de Contribuição por Plataforma

Como diferentes membros da equipe atuarão em frentes distintas (**Web**, **Desktop** e **Mobile**), siga o fluxo abaixo:

1. **Acesse a pasta de implementação**:
   ```bash
   cd Implementacao
   ```
2. **Posicione-se na branch base da sua equipe**:
   * Equipe Web: `git checkout feat/web && git pull origin feat/web`
   * Equipe Desktop: `git checkout feat/desktop && git pull origin feat/desktop`
   * Equipe Mobile: `git checkout feat/mobile && git pull origin feat/mobile`
3. **Crie uma branch de feature com nomenclatura padronizada**:
   * `feat/web/<nome-da-funcionalidade>`
   * `feat/desktop/<nome-da-funcionalidade>`
   * `feat/mobile/<nome-da-funcionalidade>`
4. **Commits padronizados e sem emojis**:
   * `git commit -m "feat(web): descricao da funcionalidade"`
5. **Push direcionado para a sua branch**:
   * `git push -u origin feat/web/<nome-da-funcionalidade>`

> Para obter instruções detalhadas, prevenção contra `detached HEAD`, perigos de `push --force` e resolução de problemas, consulte o documento completo: [**`GIT-INSTRUCTIONS.md`**](GIT-INSTRUCTIONS.md).

---

## 4. Governança e Regras de Desenvolvimento

Consulte [`Vault/README.md`](Vault/README.md) e [`Vault/00-Meta/AGENTS.md`](Vault/00-Meta/AGENTS.md) para detalhes sobre as regras de desenvolvimento, a política de **Proibido Código Sem Spec** e as diretrizes formais de documentação sem emojis.
