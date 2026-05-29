---
name: conventional-commits-ptbr
description: >
  Generate git commit messages in Brazilian Portuguese (pt-br) following the
  Conventional Commits 1.0.0 specification. Use this skill whenever the user
  asks to write, suggest, generate, or review a commit message, git commit,
  changelog entry, or describes a code change and wants a structured message.
  Also trigger when the user mentions "commit", "git message", "conventional
  commits", "mensagem de commit", "commitar", or pastes a diff/summary of
  changes. Always apply this skill even for quick one-liner commit requests —
  the structure and language rules always apply.
license: MIT
---


# Conventional Commit Message Generator (pt-br)


Generate well-structured git commit messages in **Brazilian Portuguese**, strictly following the [Conventional Commits 1.0.0](https://www.conventionalcommits.org/en/v1.0.0/) specification.

---


## Commit Structure


```
<type>[optional scope]: <description in pt-br>

[optional body in pt-br]

[optional footer(s)]
```


### Rules


1. **type** — always lowercase, required. See type list below.
2. **scope** — optional noun in parentheses describing the affected area, e.g., `feat(auth):`. Use English or the project's own naming convention for scope identifiers.
3. **`!`** — append after type/scope to signal a BREAKING CHANGE, e.g., `feat!:` or `feat(api)!:`.
4. **description** — short imperative summary in **pt-br**, written in the present tense (e.g., "adiciona", "corrige", "remove"). No period at the end. Max ~72 characters for the full first line.
5. **body** — optional, begins one blank line after the description. Free-form paragraphs in **pt-br** explaining *what* and *why*, not *how*.
6. **footers** — optional, one blank line after the body. Token format: `Token: value` or `Token #value`. Tokens use `-` in place of spaces (exception: `BREAKING CHANGE`).
7. `BREAKING CHANGE` footer **must** be uppercase and include a description of what breaks.
8. **No accents** — all pt-br text (description, body, footers) **must be written without diacritics** (no `a` with grave/acute/circumflex/tilde, no `c` with cedilla, no `e` with acute/circumflex, no `i` with acute, no `o` with acute/circumflex/tilde, no `u` with acute). This avoids encoding issues in CI/CD pipelines, git hooks, changelog generators, and external platforms. Use the unaccented form: `validacao` instead of `validacao` with cedilla, `usuario` instead of `usuario` with acute accent, etc.

---


## Commit Types


| Type | Use when | SemVer impact |
|------|----------|---------------|
| `feat` | A new feature is introduced | MINOR |
| `fix` | A bug is patched | PATCH |
| `docs` | Documentation changes only | — |
| `style` | Formatting, whitespace — no logic changes | — |
| `refactor` | Code restructuring without new features or bug fixes | — |
| `perf` | Performance improvement | — |
| `test` | Adding or correcting tests | — |
| `build` | Build system or external dependency changes | — |
| `ci` | CI/CD configuration changes | — |
| `chore` | Routine tasks, tooling, maintenance | — |
| `revert` | Reverts a previous commit | — |

> Use `BREAKING CHANGE` footer or `!` suffix on **any** type to signal a MAJOR version bump.

---


## Language Guidelines (pt-br)


- Write descriptions and body in **Brazilian Portuguese**.
- Use the **imperative present tense**: *adiciona*, *corrige*, *remove*, *atualiza*, *migra*, *melhora*, *implementa*, *refatora*, *ajusta*, *valida*, *exporta*.
- Avoid personal pronouns ("eu adicionei", "nos corrigimos").
- **No diacritics / accents** — write all pt-br text without accents or cedilla to prevent encoding issues across CI/CD pipelines, git hooks, changelog generators, and external platforms. Examples: `validacao` not `validacao` with cedilla, `usuario` not `usuario` with accent, `logica` not `logica` with accent, `notificacoes` not `notificacoes` with tilde, `servico` not `servico` with cedilla.
- Type keywords (`feat`, `fix`, `docs`, etc.), scope identifiers, and footer tokens stay in **English** — they are part of the machine-readable spec.
- `BREAKING CHANGE` stays uppercase and in English.
- Ticket/issue references stay as-is: `Refs: #123`, `Closes: #456`.

---


## Step-by-Step Generation Process


When generating a commit message, follow these steps:

1. **Understand the change**: Read the diff, description, or context provided.
2. **Classify the type**: What kind of change is this? (feature, fix, refactor, etc.)
3. **Identify the scope**: Is there a clear module, component, or area affected? (optional but recommended)
4. **Detect breaking changes**: Does this change break existing public API or behavior?
5. **Write the description line**: Concise, imperative, in pt-br, max ~72 chars total for the line.
6. **Draft the body** (if needed): Explain motivation and contrast with previous behavior. Use pt-br.
7. **Add footers** (if needed): `BREAKING CHANGE`, `Refs`, `Closes`, `Co-authored-by`, etc.
8. **Review**: Confirm the first line is under ~72 chars, no trailing period, correct type, no accents.

---


## Examples



### Simple fix


```
fix(auth): corrige validacao de token expirado
```


### New feature with scope


```
feat(carrinho): adiciona suporte a cupons de desconto
```


### Breaking change with `!` and footer


```
feat(api)!: altera formato de resposta dos endpoints de usuario

Os campos `nome` e `sobrenome` foram unificados em um unico campo `nomeCompleto`.
Clientes que consomem a API devem atualizar seus parsers.

BREAKING CHANGE: campo `nome` e `sobrenome` removidos do payload de resposta; use `nomeCompleto`
```


### Refactor with body explaining motivation


```
refactor(pagamento): extrai logica de calculo de frete para servico dedicado

A logica de frete estava acoplada ao modulo de checkout, dificultando
testes unitarios e reutilizacao em outros fluxos de compra.
O novo servico `FreteService` centraliza essas responsabilidades.
```


### Docs only


```
docs: atualiza guia de contribuicao com exemplos de commits
```


### Chore / dependency update


```
chore(deps): atualiza dependencias para versoes estaveis mais recentes
```


### Revert with references


```
revert: desfaz migracao de banco de dados da versao 2.4.0

Refs: a3f1c9b, 88d0e21
```


### Multiple footers


```
fix(relatorios): corrige calculo incorreto de totais mensais

O bug ocorria quando o mes tinha transacoes em fusos horarios diferentes.
A correcao normaliza todas as datas para UTC antes do agrupamento.

Reviewed-by: Joao Silva
Refs: #512
Closes: #489
```

---


## Output Format


Always output the commit message inside a **fenced code block** (`` ```  ```) so it is easy to copy. If there are alternative phrasings or types that could apply, briefly explain the trade-off after the code block.

```
feat(notificacoes): adiciona envio de e-mail ao completar pedido
```

> **Note:** If `feat(notificacoes)` feels too broad for your project, you could use `feat(pedido)` to scope it to the order module instead.

---


## Edge Cases & Decision Guide


| Situation | Recommendation |
|-----------|----------------|
| Change touches multiple types (e.g., fix + refactor) | Split into separate commits when possible; otherwise use the dominant type |
| Scope is unclear | Omit scope rather than guess |
| Minor visual/text fix in code | `style:` if no logic change; `fix:` if it corrects actual behavior |
| Dependency update that fixes a security issue | `fix(deps):` |
| Dependency update that adds a new capability | `feat(deps):` |
| Auto-generated or tooling change | `chore:` or `build:` |
| First commit in a new repo | `feat: inicializa projeto` is acceptable |
| Reverts with multiple SHAs | List all SHAs in `Refs:` footer |
