---
mode: agent
description: >
  Usa a skill doc-reader para extrair e interpretar conteudo de arquivos
  .doc/.docx para alimentar specs, testes e implementacao.
---

# Read DOC/DOCX (Skill: doc-reader)

Use skill `.github/skills/doc-reader/SKILL.md` para ler arquivo(s) `.doc`/`.docx`.

Entradas:
- caminho(s) dos arquivos
- objetivo (`resumo`, `extracao estruturada`, `spec`, `testes`, `regras de negocio`)

Saida esperada:
- formato definido pela skill
- origem citada por secao/heading
- ambiguidades como `Duvida / Suposicao`
- tabelas e listas preservadas em Markdown

Regras:
- nao inventar conteudo
- nao adicionar dependencias ao projeto
- nao expor dados sensiveis
