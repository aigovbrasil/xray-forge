# Example — Design Language Codex (Showroom)

eBook interativo React/JSX que percorre as 10 linguagens visuais do FORGE como capítulos navegáveis.

## O que tem

- **10 capítulos** (um por linguagem visual: Foreword, Executive Swiss, SaaS Premium, Editorial Premium, Bloomberg Terminal, Apple Product, McKinsey Consulting, Linear/Vercel, Material Design, Public Service)
- Cada capítulo contém:
  - **Style Preview** — demo interativo renderizado *naquela* linguagem visual (botões, cards, dados, código, formulários)
  - **Generative Expression** — canvas de arte algorítmica único, animado em real-time, ligado filosoficamente ao estilo
  - **Philosophy** — metadados escritos sobre origem e intenção do movimento de design
  - **Core Principles** — 4 first-principles numerados de cada sistema visual
  - **Palette Signature** — strip de cores mostrando a paleta exata do capítulo
- **Dark / Light mode** toggle — funciona em todos os capítulos
- **Sidebar colapsável** com ícones de capítulo
- **Prev/Next navigation** + barra de progresso por dots
- **Arte algorítmica** por capítulo: partículas, flow fields, matrix rain, sistemas orbitais, harmônicas de onda, pulsos de grid, hierarquias piramidais, linhas de dados, cards flutuantes, dots pulsantes
- **Brand tokens FORGE** em todo lugar: `#d97757` orange · `#6a9bcc` blue · `#788c5d` green · Poppins + Lora typography

## Como gerar

Use este prompt no Claude (skill `forge-visual-canvas` ativada):

```
/visual-canvas-studio Crie um artifact JSX (eBook interativo) que seja um showroom
das diferentes linguagens visuais e formatos catalogados, navegável, com brand
guidelines da Anthropic, modos dark e light.

Requisitos:
- Capítulo por linguagem visual (10 linguagens)
- Cada capítulo: preview ao vivo + arte algorítmica + filosofia + princípios + paleta
- Sidebar colapsável + prev/next + progress dots
- Dark/light toggle global
- Single-file React JSX bundled
- Tailwind core utilities only

Use /algorithmic-art e /canvas-design pra arte. Entregue via /web-artifacts-builder.
```

## Stack técnico

- React 18 + Vite + TypeScript
- Tailwind core utilities (sem JIT)
- Single-file HTML bundle (sem build externo no client)
- Canvas API nativo (sem libs de animação)
- Google Fonts: Poppins, Lora, JetBrains Mono, Playfair Display

## Notas

Este exemplo é o **gold standard de showroom multi-style**. Quando alguém pedir um "demo das linguagens visuais" ou um "navegador de estilos", reproduza esta estrutura de capítulos.

O HTML bundled gerado na conversa original tem ~430KB (incluindo React, Tailwind, e fonts inline). Se você gerar um novo, espere tamanho similar.

## Arquivo de referência

O artifact original gerado está disponível como `design-language-codex.html` (não incluído no zip pra economizar espaço — pode ser regenerado com o prompt acima).
