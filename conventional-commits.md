# Conventional Commits — prefixos para mensagens de Git

*Convenção prática e muito usada para mensagens de commit. Ajuda a ler o histórico e a gerar changelogs.*

---

## Formato

```
<type>(optional-scope): <short summary>
```

| Parte | Significado |
|-------|-------------|
| **type** | O tipo de alteração (prefixo). |
| **scope** (opcional) | A área/módulo afetado (ex.: api, auth, docs). |
| **summary** | Resumo curto, em imperativo e presente (“add”, “fix”, “update”). |

### Exemplos do formato completo

- `feat(api): add endpoint for user profiles`
- `fix(auth): handle expired refresh token`
- `docs(readme): add local setup instructions`

---

## Prefixos (types) mais usados

### `feat:`
**Quando:** adicionas uma nova funcionalidade (para o utilizador ou na API).

- `feat: add export to CSV`
- `feat(ui): add dark mode toggle`

### `fix:`
**Quando:** corriges um bug.

- `fix: prevent crash on empty input`
- `fix(parser): handle trailing commas`

### `docs:`
**Quando:** alterações só em documentação.

- `docs: update installation steps`
- `docs(api): document pagination parameters`

### `style:`
**Quando:** formatação que não muda comportamento (espaços, lint, etc.).

- `style: format code with ruff`
- `style(css): reorder imports`

### `refactor:`
**Quando:** reestruturas código sem mudar o comportamento externo. Não é bug fix nem feature nova.

- `refactor: extract validation helper`
- `refactor(core): simplify config loading`

### `perf:`
**Quando:** melhorias de desempenho.

- `perf: reduce query allocations`
- `perf(db): batch writes to reduce latency`

### `test:`
**Quando:** adicionas ou alteras testes.

- `test: add regression tests for login`
- `test(api): cover pagination edge cases`

### `build:`
**Quando:** alterações em ferramentas de build ou dependências (pyproject.toml, Docker, bundlers, etc.).

- `build: bump numpy to 2.x`
- `build(docker): optimize image layers`

### `ci:`
**Quando:** alterações em configuração de CI/CD (GitHub Actions, pipelines, caches).

- `ci: add mypy job`
- `ci(github): cache poetry downloads`

### `chore:`
**Quando:** tarefas de manutenção que não mudam o produto (scripts, higiene do repo, configs).

- `chore: update pre-commit hooks`
- `chore(scripts): add cleanup utility`

### `revert:`
**Quando:** revertes um commit anterior (o Git pode gerar esta mensagem automaticamente).

- `revert: feat(api): add endpoint for user profiles`

---

## Scopes (opcional)

Os scopes tornam o histórico mais legível em repositórios grandes.

*Exemplos:*
- `feat(auth): add 2FA setup flow`
- `fix(cli): handle missing config file`
- `docs(architecture): describe data pipeline`

---

## Breaking changes

Quando um commit introduz uma alteração incompatível com versões anteriores:

**Opção A:** Colocar `!` depois do type/scope

- `feat!: change config file format`
- `refactor(api)!: rename response fields`

**Opção B:** Usar um footer na mensagem

```
feat(api): change response schema

BREAKING CHANGE: `user_id` renamed to `id`.
```

---

## Exemplos de boas mensagens

| Commit | Situação |
|--------|----------|
| `feat(rssi): add bayesian filter step` | Nova funcionalidade no módulo rssi |
| `fix(time): make DST boundary tests pass` | Correção no módulo time |
| `refactor(storage): isolate dynamodb client creation` | Refactor sem mudar comportamento |
| `perf(pipe): reduce dataframe copies` | Melhoria de desempenho |
| `ci: run tests on python 3.11 and 3.12` | Alteração em CI |
| `docs: add troubleshooting section` | Só documentação |

---

## Regras simples que funcionam

1. **Resumo curto** — idealmente ≤ 72 caracteres.
2. **Verbos no imperativo** — “add”, “fix”, “remove”, “update”.
3. **Um commit = uma alteração lógica** (quando possível).
4. Preferir **`refactor:`** em vez de **`chore:`** quando estás a mudar estrutura de código.
5. **`build:`** para dependências e toolchain; **`ci:`** para pipelines e ações de CI.
