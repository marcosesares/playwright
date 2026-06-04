## PR Review Guidelines

When reviewing pull requests:

- Only comment on semantically meaningful issues: bugs, incorrect logic, security problems, or API contract violations.
- Skip style, formatting, naming, and whitespace observations unless they cause functional problems.
- Keep each comment short — one or two sentences maximum.
- Do not write long descriptions or summaries of what the code does.
- Do not suggest refactors or improvements unrelated to the PR's stated goal.
- NEVER produce a review body or top-level PR overview comment. The review body MUST be empty. Put findings only in inline comments on specific lines.


---

# Reversa

> Framework de Engenharia Reversa instalado neste projeto.

## Como usar

Digite `/reversa` para ativar o Reversa e iniciar ou retomar a análise do projeto.

## Comportamento ao ativar

Quando o usuário digitar `/reversa` ou a palavra `reversa` sozinha em uma mensagem:

1. Ative o skill `reversa` disponível em `.agents/skills/reversa/SKILL.md`
2. Leia o SKILL.md na íntegra e siga exatamente as instruções do Reversa

## Regra não-negociável

Nunca apague, modifique ou sobrescreva arquivos pré-existentes do projeto legado.
O Reversa escreve **apenas** em `.reversa/` e `_reversa_sdd/`.
