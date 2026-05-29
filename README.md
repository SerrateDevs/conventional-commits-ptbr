# conventional-commits-ptbr

[![skills.sh](https://skills.sh/b/SerrateDevs/conventional-commits-ptbr)](https://skills.sh/SerrateDevs/conventional-commits-ptbr)
![License: MIT](https://img.shields.io/badge/license-MIT-blue.svg)
![Conventional Commits](https://img.shields.io/badge/conventional%20commits-1.0.0-yellow.svg)
![Language](https://img.shields.io/badge/lang-pt--br-green.svg)

Skill que gera mensagens de commit git em **portugues brasileiro**, seguindo rigorosamente a especificacao [Conventional Commits 1.0.0](https://www.conventionalcommits.org/en/v1.0.0/). Compativel com qualquer agente que suporte a [Agent Skills spec](https://agentskills.io): Claude Code, Cursor, Codex, Windsurf, Gemini CLI, Roo Code, e [dezenas de outros](https://agentskills.io/clients).

## Instalacao

### Via `npx skills` (qualquer agente)

```bash
npx skills add SerrateDevs/conventional-commits-ptbr
```

Instala automaticamente para todos os agentes detectados. Para um agente especifico:

```bash
npx skills add SerrateDevs/conventional-commits-ptbr -a claude-code
npx skills add SerrateDevs/conventional-commits-ptbr -a cursor
npx skills add SerrateDevs/conventional-commits-ptbr -a opencode
```

### Via opencode

```bash
opencode skill install serratedev/conventional-commits-ptbr
```

### Instalacao manual

Copie o diretorio para a pasta de skills do seu agente:

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
<type>[scope]: <descricao em pt-br>

[body opcional em pt-br]

[footers opcionais]
```

### Gatilhos automaticos

A skill e ativada automaticamente quando voce menciona:

- "commit", "commitar", "mensagem de commit"
- "git message", "conventional commits"
- Pede para escrever, sugerir ou revisar uma mensagem de commit
- Descreve uma mudanca de codigo e quer uma mensagem estruturada

## Tipos de commit

| Type | Uso | Impacto SemVer |
|------|-----|----------------|
| `feat` | Nova funcionalidade | MINOR |
| `fix` | Correcao de bug | PATCH |
| `docs` | Mudancas em documentacao | — |
| `style` | Formatacao, espacamento — sem mudanca de logica | — |
| `refactor` | Reestruturacao sem nova feature ou fix | — |
| `perf` | Melhoria de performance | — |
| `test` | Adicao ou correcao de testes | — |
| `build` | Sistema de build ou dependencias externas | — |
| `ci` | Configuracao de CI/CD | — |
| `chore` | Tarefas rotineiras, ferramentas, manutencao | — |
| `revert` | Reverte um commit anterior | — |

## Exemplos

### Fix simples

```
fix(auth): corrige validacao de token expirado
```

### Feature com scope

```
feat(carrinho): adiciona suporte a cupons de desconto
```

### Breaking change

```
feat(api)!: altera formato de resposta dos endpoints de usuario

Os campos `nome` e `sobrenome` foram unificados em um unico campo `nomeCompleto`.
Clientes que consomem a API devem atualizar seus parsers.

BREAKING CHANGE: campo `nome` e `sobrenome` removidos do payload de resposta; use `nomeCompleto`
```

### Refactor com body

```
refactor(pagamento): extrai logica de calculo de frete para servico dedicado

A logica de frete estava acoplada ao modulo de checkout, dificultando
testes unitarios e reutilizacao em outros fluxos de compra.
O novo servico `FreteService` centraliza essas responsabilidades.
```

### Dependencia

```
chore(deps): atualiza dependencias para versoes estaveis mais recentes
```

### Revert com referencias

```
revert: desfaz migracao de banco de dados da versao 2.4.0

Refs: a3f1c9b, 88d0e21
```

## Regras de linguagem

- Descricoes e bodies em **portugues brasileiro**
- Voz **imperativa presente**: *adiciona*, *corrige*, *remove*, *atualiza*
- **Sem acentos** — todo texto em pt-br deve ser escrito sem diacriticos para evitar problemas de encoding em pipelines CI/CD, git hooks e plataformas externas. Exemplos: `validacao` (nao `validacao` com cedilha), `usuario` (nao `usuario` com acento), `logica` (nao `logica` com acento)
- Sem pronomes pessoais ("eu adicionei", "nos corrigimos")
- Types, scopes e footer tokens permanecem em **ingles** (parte da spec)
- `BREAKING CHANGE` permanece em ingles e maiusculo

## Licenca

[MIT](./LICENSE)
