# Projeto Integrado Multidisciplinar (PIM IV) - E-Commerce Omnichannel

> Repositório agregador e orquestrador do projeto PIM IV, conectando a governança documental e a implementação dos sistemas Web, Desktop e Mobile através de submódulos Git.

---

## 1. Estrutura do Ecossistema

```text
PIM/
├── .gitmodules             # Definição e mapeamento dos submódulos remotos
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

## 3. Branches e Fluxo de Desenvolvimento

O repositório `Implementacao` adota o seguinte modelo de ramificações:
* `feat/web`: Desenvolvimento do sistema Web (ASP.NET Core MVC).
* `feat/desktop`: Desenvolvimento do sistema Desktop (PDV / Hardware local).
* `feat/mobile`: Desenvolvimento do sistema Mobile (App).
* `develop`: Branch de integração e testes conjuntos.
* `production`: Branch de entrega final consolidada e homologada.

---

## 4. Governança e Regras de Desenvolvimento

Consulte [`Vault/README.md`](file:///c:/Users/vinic/Documents/PIM/Vault/README.md) e [`Vault/00-Meta/AGENTS.md`](file:///c:/Users/vinic/Documents/PIM/Vault/00-Meta/AGENTS.md) para detalhes sobre as regras de desenvolvimento, a política de Proibido Código Sem Spec e as diretrizes formais de documentação sem emojis.
