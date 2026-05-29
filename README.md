# conventional-commits-ptbr

[![skills.sh](https://skills.sh/b/SerrateDevs/conventional-commits-ptbr)](https://skills.sh/SerrateDevs/conventional-commits-ptbr)
![License: MIT](https://img.shields.io/badge/license-MIT-blue.svg)
![Conventional Commits](https://img.shields.io/badge/conventional%20commits-1.0.0-yellow.svg)
![Language](https://img.shields.io/badge/lang-pt--br-green.svg)

Skill que gera mensagens de commit git em **português brasileiro**, seguindo rigorosamente a especificação [Conventional Commits 1.0.0](https://www.conventionalcommits.org/en/v1.0.0/). Compatível com qualquer agente que suporte a [Agent Skills spec](https://agentskills.io): Claude Code, Cursor, Codex, Windsurf, Gemini CLI, Roo Code, e [dezenas de outros](https://agentskills.io/clients).

## Instalação

### Via `npx skills` (qualquer agente)

```bash
npx skills add SerrateDevs/conventional-commits-ptbr
```

Instala automaticamente para todos os agentes detectados. Para um agente específico:

```bash
npx skills add SerrateDevs/conventional-commits-ptbr -a claude-code
npx skills add SerrateDevs/conventional-commits-ptbr -a cursor
npx skills add SerrateDevs/conventional-commits-ptbr -a opencode
```

### Via opencode

```bash
opencode skill install serratedev/conventional-commits-ptbr
```

### Instalação manual

Copie o diretório para a pasta de skills do seu agente:

```bash
git clone https://github.com/SerrateDevs/conventional-commits-ptbr.git
# Para opencode / cline / codex / amp / etc.:
cp -r conventional-commits-ptbr ~/.agents/skills/conventional-commits-ptbr
# Para Claude Code:
cp -r conventional-commits-ptbr ~/.claude/skills/conventional-commits-ptbr
# Para Cursor:
cp -r conventional-commits-ptbr ~/.cursor/skills/conventional-commits-ptbr
```

## O que faz

Quando ativada, a skill faz o opencode gerar mensagens de commit estruturadas em pt-br no formato:

```
<type>[scope]: <descrição em pt-br>

[body opcional em pt-br]

[footers opcionais]
```

### Gatilhos automáticos

A skill é ativada automaticamente quando você menciona:

- "commit", "commitar", "mensagem de commit"
- "git message", "conventional commits"
- Pede para escrever, sugerir ou revisar uma mensagem de commit
- Descreve uma mudança de código e quer uma mensagem estruturada

## Tipos de commit

| Type | Uso | Impacto SemVer |
|------|-----|----------------|
| `feat` | Nova funcionalidade | MINOR |
| `fix` | Correção de bug | PATCH |
| `docs` | Mudanças em documentação | — |
| `style` | Formatação, espaçamento — sem mudança de lógica | — |
| `refactor` | Reestruturação sem nova feature ou fix | — |
| `perf` | Melhoria de performance | — |
| `test` | Adição ou correção de testes | — |
| `build` | Sistema de build ou dependências externas | — |
| `ci` | Configuração de CI/CD | — |
| `chore` | Tarefas rotineiras, ferramentas, manutenção | — |
| `revert` | Reverte um commit anterior | — |

## Exemplos

### Fix simples

```
fix(auth): corrige validação de token expirado
```

### Feature com scope

```
feat(carrinho): adiciona suporte a cupons de desconto
```

### Breaking change

```
feat(api)!: altera formato de resposta dos endpoints de usuário

Os campos `nome` e `sobrenome` foram unificados em um único campo `nomeCompleto`.
Clientes que consomem a API devem atualizar seus parsers.

BREAKING CHANGE: campo `nome` e `sobrenome` removidos do payload de resposta; use `nomeCompleto`
```

### Refactor com body

```
refactor(pagamento): extrai lógica de cálculo de frete para serviço dedicado

A lógica de frete estava acoplada ao módulo de checkout, dificultando
testes unitários e reutilização em outros fluxos de compra.
O novo serviço `FreteService` centraliza essas responsabilidades.
```

### Dependência

```
chore(deps): atualiza dependências para versões estáveis mais recentes
```

### Revert com referências

```
revert: desfaz migração de banco de dados da versão 2.4.0

Refs: a3f1c9b, 88d0e21
```

## Regras de linguagem

- Descrições e bodies em **português brasileiro**
- Voz **imperativa presente**: *adiciona*, *corrige*, *remove*, *atualiza*
- Sem pronomes pessoais ("eu adicionei", "nós corrigimos")
- Types, scopes e footer tokens permanecem em **inglês** (parte da spec)
- `BREAKING CHANGE` permanece em inglês e maiúsculo

## Licença

[MIT](./LICENSE)
