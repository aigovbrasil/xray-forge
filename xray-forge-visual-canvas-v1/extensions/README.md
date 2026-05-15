# Extensions — Slot pra você adicionar habilidades

Este diretório é onde você (João) adiciona **novos artifacts, linguagens visuais ou referências** sem mexer no core da skill.

## Por que separar

Manter `references/` e `assets/` como **núcleo estável** garante que o sistema funcione mesmo enquanto você experimenta. Extensions é seu laboratório — pode quebrar, refazer, descartar.

Quando uma extensão amadurecer e você quiser promover ao core:
1. Mova o arquivo de `extensions/<nome>/` pra `references/` ou `assets/` conforme apropriado
2. Atualize o SKILL.md mestre com link/menção
3. Atualize o CHANGELOG.md

## Estrutura padrão de uma extensão

```
extensions/
└── <nome-da-extensao>/
    ├── SKILL.md              # frontmatter + descrição curta + quando usar
    ├── README.md             # docs longas (opcional)
    ├── assets/               # arquivos referenciados (opcional)
    │   └── ...
    └── examples/             # exemplos gerados (opcional)
        └── ...
```

## Template: SKILL.md de extensão

```markdown
---
name: forge-ext-<nome-da-extensao>
description: <O que essa extensão faz, com triggers PT-BR e EN. Seja "pushy" — mencione quando ativar e quando NÃO ativar.>
version: 0.1.0
parent: forge-visual-canvas
---

# <Nome da Extensão>

<Resumo de 2-3 linhas>

## Quando ativa

- Trigger 1 (PT-BR)
- Trigger 2 (EN)
- ...

## O que entrega

<Output específico>

## Como difere do core

<Por que essa extensão não está no core e quando você prefere ela>

## Dependências

- Herda tokens de `../../references/brand-tokens.md`
- Herda linguagens visuais de `../../references/visual-languages.md`
- (outras se aplicável)

## Exemplos

- `examples/exemplo1.html` — descrição
```

## Ideias de extensões pra João adicionar (v2 backlog)

Sugestões baseadas no perfil de consultor presencial em PT-BR:

### 1. `proposta-comercial-pme`
Template de proposta comercial em A4 com:
- Capa com logo do cliente
- Diagnóstico (problema + impacto)
- Solução proposta
- Cronograma
- Investimento
- Termos
- Página de assinatura

### 2. `diagnostico-presencial`
Artifact de **uso ao vivo** durante reunião presencial:
- Tela cheia, font grande
- Inputs do consultor preenchem em tempo real
- Cliente vê o diagnóstico se montando
- Export pra PDF no final da reunião

### 3. `playbook-cliente-personalizado`
Documento operacional pós-projeto:
- SOPs do dia-a-dia do cliente
- Métricas pra acompanhar
- Quando voltar pra consultoria
- White-label com a marca da Maia Consultoria

### 4. `dashboard-acompanhamento`
Painel mensal pro cliente:
- KPIs do projeto
- Status de iniciativas
- Próximas reuniões
- Histórico de decisões

### 5. `apresentacao-fechamento`
Deck PPTX de fechamento de projeto consultivo:
- O que foi feito
- Resultados mensuráveis
- Próximos passos
- Proposta de continuidade

### 6. `linguagens-visuais-extra`
Linguagens não catalogadas no core mas que você usa:
- Estilo "Maia Consultoria" próprio (paleta + fontes da sua marca)
- Estilo "cliente X" (quando recorrente)
- Adapt de algum estilo do core pra realidade brasileira

### 7. `templates-whatsapp`
Não é visual, mas se quiser: templates de mensagem pós-reunião que viram cards visuais quando o cliente compartilha.

---

## Convenção de nomes

- Sempre prefixo `forge-ext-` no name do frontmatter
- Diretório com nome curto, kebab-case: `extensions/proposta-comercial/`
- Versão começa em 0.1.0 e sobe conforme estabiliza

## Como testar uma extensão

1. Crie a estrutura em `extensions/<nome>/`
2. Escreva o SKILL.md da extensão
3. Pede pro Claude algo que deveria triggar a extensão
4. Veja se ele referencia o arquivo certo
5. Itere no description ate triggar consistente

## Não fazer

- ❌ Sobrescrever tokens canônicos (`brand-tokens.md`) numa extensão — herde e estenda
- ❌ Criar uma extensão que duplica algo do core — proponha edit no core via CHANGELOG
- ❌ Hardcodar paleta diferente da FORGE sem documentar o motivo
