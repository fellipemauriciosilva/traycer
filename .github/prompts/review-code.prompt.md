---
mode: agent
description: >
  Executa code review estruturado com foco em risco, regressao e aderencia a spec,
  com checklist por stack.
---

# Review Code

Revise as mudancas atuais com base em specs, instructions e arquitetura do projeto.

## Entradas esperadas

- Projeto alvo: `[PROJETO]`
- Ticket relacionado (se existir): `[TICKET]`

## O que revisar

### 1. Alinhamento com a spec
- escopo implementado corresponde ao pedido
- criterios de aceite cobertos
- regras de negocio preservadas
- contratos publicos preservados (REST, DTO, mensageria, banco)

### 2. Arquitetura
- separacao de camadas respeitada
- controllers finos
- logica de dominio fora de repositorio/controller
- integracoes externas isoladas em clients/adapters
- sem dependencia nova sem justificativa

### 3. Checklist por stack

Java/Spring:
- injecao por construtor
- sem `@SpringBootTest` em teste unitario
- `@WebMvcTest` para controller unitario
- SQL parametrizado (JDBI/JPA)
- logs sem dados sensiveis

.NET:
- `async/await` correto (sem `.Result`/`.Wait()`)
- `CancellationToken` propagado quando aplicavel
- SQL parametrizado
- logs sem segredos
- testes unitarios sem subir contexto completo

### 4. Testes
- cobertura de comportamento alterado
- happy path, validacao, falhas externas, edge cases
- nomes de teste claros
- sem mock da classe sob teste

### 5. Seguranca e observabilidade
- sem credenciais/segredos no codigo
- tratamento de erro sem vazar infraestrutura no response
- logs suficientes para diagnostico

## Formato de saida (obrigatorio)

```md
## Summary
## Changes
## Tests
## Risks
## Validation
## Related Spec
```

## Severidade dos achados

- CRITICO: precisa corrigir antes do merge
- MELHORIA: recomendado corrigir
- SUGESTAO: opcional
- OK: sem problema

## Pos-review

Se houver `[TICKET]`, atualizar `[PROJETO]/.github/docs/specs/[TICKET]/status.md`:

```markdown
| Passo atual | 5 - Revisada |
| Proximo passo | 6 - Concluida |
| Proximo agent | Abrir PR |
```

Adicionar historico:

```markdown
| 5 | Revisada | `/review-code` | [DATA DE HOJE] |
```

Exibir:

```
PROXIMO PASSO -> Abrir Pull Request
```
