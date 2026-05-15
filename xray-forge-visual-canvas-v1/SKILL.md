# X-RAY SUITE · xray-forge-visual-canvas-v1

---
name: forge-visual-canvas
description: Sistema FORGE para gerar artifacts visuais premium (HTML, React/JSX, SVG, PDF, PPTX) com brand consistency, dark/light mode, e troca de linguagem visual em runtime. ATIVE SEMPRE para "criar artifact", "gerar showroom", "design language codex", "modal clone", "página de venda", "apresentação executiva", "ebook interativo", "diagrama profissional", "PDF estratégico A4", "playbook visual", "FORGE", "visual canvas studio", "brand guidelines Anthropic", "modo dark e light", ou pedidos de UI premium estilo Stripe/Linear/Vercel/McKinsey/Bloomberg/Apple/GOV.UK. TAMBÉM ATIVE quando o pedido envolver clone pixel-perfect de uma referência visual, ou quando o usuário pedir "estilo executivo", "estilo SaaS", "estilo editorial", "estilo dashboard", "estilo terminal", ou qualquer das 10 linguagens visuais catalogadas. NÃO ATIVE para tarefas puras de texto, código backend, ou perguntas conceituais sem entregável visual.
version: 2.0.0
author: João Maia (Maia Consultoria) + FORGE
---

# FORGE Visual Canvas

Sistema canônico para produzir artifacts visuais de nível agência — sem "AI slop", sem gradientes roxos, sem Inter font genérica.

**Pipeline de 3 camadas que rodam em sequência em todo output:**

```
estrutura  →  tokens  →  acabamento
(formato)    (brand)    (mood)
```

1. **Estrutura** — escolher o formato certo (HTML widget, React JSX, SVG inline, PDF A4, PPTX, etc.)
2. **Tokens** — aplicar brand FORGE (paleta + tipografia + shape rules) — fonte da verdade absoluta
3. **Acabamento** — escolher a linguagem visual entre as 10 catalogadas, ajustar densidade, dark/light

---

## Quando este skill ativa

Triggers em PT-BR (operação principal do João):
- "criar artifact", "gerar artifact"
- "gerar showroom", "ebook interativo", "design codex"
- "modal clone", "clone pixel-perfect", "réplica exata"
- "página de venda", "landing page premium"
- "apresentação executiva", "deck McKinsey", "playbook"
- "PDF A4 estratégico", "documento executivo multi-página"
- "diagrama profissional", "infográfico"
- "estilo executivo / SaaS / editorial / dashboard / terminal / Apple / GOV.UK"
- "modo dark e light", "trocar de tema"

Triggers em EN (compatibilidade com prompts copiados):
- "FORGE", "visual canvas studio"
- "brand guidelines", "Anthropic brand"
- "production-grade artifact", "strategy-grade visual"

---

## Decision tree — qual formato de output

```
Pedido recebido
│
├─ É um modal / card / componente UI isolado?
│   └─ HTML widget single-file via show_widget OU artifact .html
│       Use: assets/excel-modal-clone.html como gold standard
│
├─ É um diagrama / fluxo / arquitetura?
│   └─ SVG inline (Poppins/Lora labels, paleta brand)
│
├─ É app multi-tela / dashboard / showroom interativo?
│   └─ React JSX artifact (Tailwind core utilities)
│       Use: examples/design-language-codex/ como referência
│
├─ É um documento PDF A4 multi-página (relatório, manifesto)?
│   └─ HTML com <div class="a4-page"> + <svg viewBox="0 0 794 1123">
│       Use: references/svg-document-engine.md (templates prontos)
│
├─ É deck / apresentação?
│   └─ Ler /mnt/skills/public/pptx/SKILL.md → python-pptx + brand colors
│
├─ É documento Word?
│   └─ Ler /mnt/skills/public/docx/SKILL.md → python-docx + Poppins/Lora
│
└─ Pedido envolve TROCA de linguagem visual em runtime?
    └─ Master Prompt Template (assets/master-prompt-engine.md)
       — control panel com 4 selectors (style/component/density/theme)
```

---

## Brand FORGE — fonte da verdade

A paleta e tipografia abaixo são **não-negociáveis**. Toda saída usa CSS variables — nunca hardcode.

```css
/* Surfaces */
--forge-dark:       #141413;  /* texto primário, bg dark */
--forge-light:      #faf9f5;  /* bg light, texto on dark */
--forge-mid-gray:   #b0aea5;  /* secundário, muted */
--forge-light-gray: #e8e6dc;  /* bg subtle, borders */

/* Acentos — usar nesta ordem ao colorir múltiplos elementos */
--forge-orange: #d97757;  /* acento primário — CTAs, highlights */
--forge-blue:   #6a9bcc;  /* acento secundário — links, info */
--forge-green:  #788c5d;  /* acento terciário — success, tags */

/* Tipografia */
--forge-heading: 'Poppins', Arial, sans-serif;
--forge-body:    'Lora', Georgia, serif;
--forge-mono:    'JetBrains Mono', 'SF Mono', Consolas, monospace;
```

**Regras de forma:**
- Border radius: 4px default, 8px cards, 12px cards grandes, 20px modais, 9999px pills
- Sem gradientes em elementos decorativos
- Sombras só funcionais (modais e cards elevados)
- Pesos permitidos: 400, 500, 700, 800 — **nunca 600**
- Font-size mínimo: 11px

Detalhes completos: **[references/brand-tokens.md](references/brand-tokens.md)**

---

## As 10 linguagens visuais catalogadas

| # | Linguagem | Quando usar |
|---|---|---|
| 1 | Executive Swiss | Relatórios C-level, propostas, diagnósticos B2B |
| 2 | SaaS Premium | Landing pages, produtos AI-first, MVPs |
| 3 | Enterprise Dashboard | Painéis ops, BI, monitoramento dense |
| 4 | Public Service (GOV.UK) | Formulários, onboarding, fluxos consultivos |
| 5 | Editorial Premium | Manifestos, whitepapers, conteúdo de autoridade |
| 6 | McKinsey Consulting | Due diligence, board presentations, M&A |
| 7 | Bloomberg Terminal | Trading dashboards, cockpit financeiro dense |
| 8 | Apple Product | Apps consumer, onboarding premium |
| 9 | Material Design | Apps Android, sistemas com elevação |
| 10 | Linear/Vercel | Dev tools, ferramentas técnicas modernas |

Specs completas (paleta, tipografia, layout, prompt trigger): **[references/visual-languages.md](references/visual-languages.md)**

---

## Sistemas de componentes (independentes da linguagem visual)

São 5 sistemas que definem como botões, cards, tables e badges são construídos:

- **C1. shadcn/ui inspired** (default) — bordas finas, cards arredondados
- **C2. Tailwind Utility** — utility-first, sem abstrações
- **C3. IBM Carbon** — bordas duras, square corners, full-grid tables
- **C4. Material Design** — sombras de elevação, FABs, ripple effects
- **C5. Ant Design** — tags coloridas, formulários com label-acima

Detalhes + matriz de combinação ideal (linguagem × componente): **[references/component-systems.md](references/component-systems.md)**

---

## Master Prompt Engine — gerador parametrizável

Pra criar artifacts onde o **conteúdo é fixo** mas a **linguagem visual é trocável em runtime** via control panel (4 selectors: style / component / density / theme).

Template completo, copy-paste-ready: **[assets/master-prompt-engine.md](assets/master-prompt-engine.md)**

Como usar:
1. Abrir `assets/master-prompt-engine.md`
2. Substituir o bloco `BUSINESS_CASE` pelo seu conteúdo
3. Colar o prompt inteiro no Claude
4. Receber single-file HTML com selectors funcionais + calculator + SVG charts

---

## SVG Document Engine — PDFs A4 multi-página

Pra gerar relatórios, manifestos, playbooks A4 que exportam direto pra PDF via "Imprimir → Salvar como PDF" (sem libs externas).

Arquitetura: `<div class="a4-page">` + `<svg viewBox="0 0 794 1123">` (A4 a 96dpi).

Templates de página + global SVG defs (ícones, gradientes, patterns) prontos: **[references/svg-document-engine.md](references/svg-document-engine.md)**

---

## Anti-patterns — nunca fazer

- Gradientes roxos como background
- Inter font (default "AI slop" — usar Poppins)
- Cantos arredondados uniformes em tudo
- Cores hardcoded que quebram dark mode
- `position:fixed` em widgets show_widget (colapsa o iframe)
- Emoji decorativo (usar SVG paths ou shapes CSS)
- Font-size abaixo de 11px
- Font-weight 600
- `<html>`, `<head>`, `<body>` em show_widget
- Drop shadows decorativos, blur, glow, neon

---

## Como estender (slot pra v2+ do João)

Adicione novos artifacts, linguagens visuais ou referências em **`extensions/`**.

Convenção:
- `extensions/<nome-da-extensao>/SKILL.md` — descrição curta + quando usar
- `extensions/<nome-da-extensao>/assets/` — arquivos referenciados
- Linkar no SKILL.md mestre na seção "Extensões instaladas" (abaixo)

Veja **[extensions/README.md](extensions/README.md)** para o template e regras.

### Extensões instaladas

_Nenhuma ainda. Adicione a sua primeira em `extensions/`._

---

## Exemplo de referência

**[examples/design-language-codex/](examples/design-language-codex/)** — eBook interativo React/JSX que percorre as 10 linguagens com arte algorítmica por capítulo, dark/light mode, sidebar navegável. Use como gold standard de showroom multi-style.

---

## Pipeline de execução (resumo operacional)

Ao receber um pedido que ative este skill:

1. **Identificar formato** (decision tree acima) → escolher entre HTML widget, React JSX, SVG, PDF A4, PPTX, DOCX
2. **Carregar tokens** → ler `references/brand-tokens.md` se houver dúvida sobre paleta/tipografia
3. **Escolher linguagem visual** → consultar `references/visual-languages.md` se o pedido nomear estilo específico
4. **Escolher sistema de componentes** → consultar `references/component-systems.md` se for app/dashboard
5. **Aplicar dark/light** → CSS variables sempre, nunca hardcoded
6. **Lint mental antes de entregar:**
   - Toda cor é variável CSS? ✓
   - Toda fonte é Poppins/Lora/Mono? ✓
   - Algum gradiente decorativo? ✗
   - Algum font-weight 600? ✗
   - Funciona em dark mode? ✓
7. **Entregar** → via `present_files` (artifact) ou `show_widget` (inline)

---

*FORGE Visual Canvas v2.0 — same logic, variable visual system.*
