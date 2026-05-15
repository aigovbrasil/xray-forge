# FORGE Visual Canvas — v2.0.0

Sistema canônico para gerar artifacts visuais premium (HTML, React/JSX, SVG, PDF A4 multi-página, PPTX) com brand consistency, dark/light mode, e troca de linguagem visual em runtime.

**Mantenedor:** João Maia (Maia Consultoria)
**Origem:** consolidação dos materiais FORGE Brand System + Visual Canvas Studio + SVG Document Engine + Design Language Codex
**Modo de operação:** consultoria guiada em linguagem acessível com cliente presencial

---

## O que esta skill faz

Quando você (ou um cliente seu) pede um artifact visual, o Claude:
1. **Identifica o formato certo** (HTML widget, React JSX, SVG inline, PDF A4, deck PPTX, doc Word) via decision tree
2. **Aplica os brand tokens FORGE** (paleta + tipografia + shape rules) — nunca hardcoded
3. **Escolhe a linguagem visual adequada** entre 10 catalogadas (Executive Swiss, SaaS Premium, McKinsey, Bloomberg, Apple, GOV.UK, Editorial, etc.)
4. **Aplica o sistema de componentes** correto (shadcn/ui, Carbon, Material, Ant, Tailwind)
5. **Garante dark/light mode** funcionando
6. **Entrega** sem "AI slop" (sem gradiente roxo, sem Inter, sem font-weight 600, sem cantos arredondados em tudo)

## Estrutura de pastas

```
forge-visual-canvas/
├── SKILL.md                       ← entry point (Claude lê primeiro)
├── README.md                      ← este arquivo
├── CHANGELOG.md                   ← histórico de versões e auditoria v1→v2
│
├── references/                    ← consultadas por demanda durante execução
│   ├── brand-tokens.md            ← FONTE DA VERDADE: paleta, tipografia, shape rules
│   ├── visual-languages.md        ← 10 linguagens detalhadas (paleta + layout + prompt trigger)
│   ├── component-systems.md       ← 5 sistemas de componente + matriz de combinação
│   └── svg-document-engine.md     ← templates A4 multi-página pra PDFs
│
├── assets/                        ← arquivos canônicos referenciados nos outputs
│   ├── master-prompt-engine.md    ← prompt parametrizável copy-paste pra gerar canvas studios
│   └── excel-modal-clone.html     ← gold standard de modal clone (referência pixel-perfect)
│
├── examples/                      ← exemplos de referência
│   └── design-language-codex/     ← showroom interativo das 10 linguagens (eBook React)
│       └── README.md              ← como regenerar e o que tem
│
└── extensions/                    ← SLOT PRA VOCÊ (João) adicionar habilidades
    ├── README.md                  ← guia + 7 ideias de extensões pro v2 backlog
    └── .gitkeep                   ← placeholder
```

## Como instalar

1. Faça upload de toda a pasta `forge-visual-canvas/` (com seus arquivos) como skill no Claude
2. Verifique que o YAML frontmatter do `SKILL.md` está válido (name + description preenchidos)
3. Teste com um trigger:
   - "FORGE: cria um modal clone do meu produto"
   - "Gera um showroom das linguagens visuais"
   - "Quero um PDF A4 estratégico do diagnóstico"

## Como adicionar suas próprias habilidades (v2)

Veja **[extensions/README.md](extensions/README.md)** — tem o template completo + 7 ideias específicas pra consultor PT-BR (proposta comercial, diagnóstico presencial, playbook cliente, etc.).

**Resumo:**
1. Cria pasta em `extensions/sua-habilidade/`
2. Coloca `SKILL.md` com frontmatter (`name: forge-ext-sua-habilidade`, `parent: forge-visual-canvas`)
3. Adiciona assets/examples se precisar
4. Linka no SKILL.md mestre na seção "Extensões instaladas"

## Quick start — testes rápidos

### Teste 1: trigger básico
Prompt: `Cria um modal de onboarding do meu app de gestão financeira PME, estilo SaaS Premium em modo dark.`

Esperado: HTML widget single-file usando paleta SaaS Premium dark mode + tokens FORGE.

### Teste 2: PDF A4 estratégico
Prompt: `Gera um relatório executivo A4 de 4 páginas sobre estratégia de pricing, com capa dark, sumário, análise e recomendações. Estilo McKinsey.`

Esperado: HTML com 4 `<div class="a4-page">` usando templates do `svg-document-engine.md`.

### Teste 3: showroom multi-style
Prompt: `Cria um eBook interativo React mostrando todas as linguagens visuais catalogadas, com toggle dark/light e sidebar.`

Esperado: artifact JSX similar ao `examples/design-language-codex/`.

## Princípios não-negociáveis

- ✅ Brand tokens FORGE são fonte da verdade — `brand-tokens.md` vence em conflito com qualquer outro doc
- ✅ Dark mode obrigatório em todo artifact
- ✅ CSS variables ao invés de hex hardcoded
- ✅ Poppins (heading) + Lora (body) + JetBrains Mono (code/data)
- ❌ Sem gradiente roxo de fundo
- ❌ Sem Inter font (default "AI slop")
- ❌ Sem font-weight 600
- ❌ Sem cantos arredondados em tudo
- ❌ Sem `position:fixed` em show_widget

## Suporte

Se a skill não estiver triggando como esperado, ajuste o `description:` no SKILL.md mestre — adicione phrasings em PT-BR específicos do seu vocabulário de consultoria. O Claude usa `description` como mecanismo primário de triggering.

Se um cliente seu pedir algo fora das linguagens catalogadas, considere criar uma extensão custom pra ele em `extensions/cliente-x/`.
