---
mode: agent
description: >
  Usa a skill pdf-reader para extrair e interpretar conteudo de PDF para
  alimentar specs, testes e implementacao.
---

# Read PDF (Skill: pdf-reader)

Use skill `.github/skills/pdf-reader/SKILL.md` para ler PDF(s) informados.

Entradas:
- caminho(s) dos arquivos
- objetivo (`resumo`, `extracao estruturada`, `spec`, `testes`, `regras de negocio`)

Saida esperada:
- formato definido pela skill
- origem citada por pagina (`p. N`)
- ambiguidades como `Duvida / Suposicao`

Regras:
- nao inventar conteudo
- nao adicionar dependencias ao projeto
- nao expor dados sensiveis
