# SVG Document Engine — PDFs A4 Multi-Página

Arquitetura para gerar documentos A4 paginados que exportam direto pra PDF via "Imprimir → Salvar como PDF" — sem libs externas.

**Padrão:** cada página = `<div class="a4-page">` contendo `<svg viewBox="0 0 794 1123">`.
794 × 1123 pixels = A4 a 96dpi.
`@media print` resolve a exportação nativa.

---

## 1. Page setup (HTML base)

```html
<!DOCTYPE html>
<html lang="pt-BR">
<head>
  <meta charset="UTF-8">
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link href="https://fonts.googleapis.com/css2?family=JetBrains+Mono:wght@400;700&family=Lora:ital,wght@0,400;0,700;1,400&family=Poppins:wght@400;500;700;800&family=Playfair+Display:wght@700;900&display=swap" rel="stylesheet">
  <style>
    * { box-sizing: border-box; margin: 0; padding: 0; }
    body {
      background: #e0e5ec;
      font-family: 'Poppins', sans-serif;
      display: flex; flex-direction: column; align-items: center;
      gap: 40px; padding: 40px 0;
      -webkit-font-smoothing: antialiased;
    }
    .a4-page {
      width: 210mm; height: 297mm;
      background: #fff;
      box-shadow: 0 15px 35px rgba(0,0,0,0.15);
      position: relative; overflow: hidden; flex-shrink: 0;
    }
    svg.page-svg {
      width: 100%; height: 100%;
      position: absolute; top: 0; left: 0;
    }
    @page { size: A4; margin: 0; }
    @media print {
      body { background: none; padding: 0; gap: 0; display: block; }
      .a4-page { box-shadow: none; break-after: page; }
    }
  </style>
</head>
<body>
  <!-- inserir SVG defs globais aqui (ver seção 2) -->
  <!-- inserir páginas aqui (ver seção 3) -->
</body>
</html>
```

---

## 2. Global SVG defs (compartilhado por todas as páginas)

Inserir **uma vez** antes da primeira página. Todas as páginas referenciam por ID.

```html
<svg width="0" height="0" style="position:absolute;">
  <defs>

    <!-- TEXTURA: ruído sutil (efeito anti-AI, organicidade) -->
    <filter id="noise">
      <feTurbulence type="fractalNoise" baseFrequency="0.8" numOctaves="3" stitchTiles="stitch"/>
      <feColorMatrix type="matrix" values="1 0 0 0 0  0 1 0 0 0  0 0 1 0 0  0 0 0 0.04 0"/>
      <feComposite operator="in" in2="SourceGraphic" result="mn"/>
      <feBlend in="SourceGraphic" in2="mn" mode="multiply"/>
    </filter>

    <!-- SHADOW: somente funcional -->
    <filter id="shadow" x="-10%" y="-10%" width="130%" height="130%">
      <feDropShadow dx="0" dy="6" stdDeviation="12" flood-color="#000" flood-opacity="0.08"/>
    </filter>

    <!-- GRADIENTES: paleta corporativa FORGE -->
    <linearGradient id="grad-dark" x1="0%" y1="0%" x2="100%" y2="100%">
      <stop offset="0%" style="stop-color:#1a365d"/>
      <stop offset="100%" style="stop-color:#0a1526"/>
    </linearGradient>
    <linearGradient id="grad-accent" x1="0%" y1="0%" x2="100%" y2="0%">
      <stop offset="0%" style="stop-color:#d97757"/>
      <stop offset="100%" style="stop-color:#e8956d"/>
    </linearGradient>
    <linearGradient id="grad-light" x1="0%" y1="0%" x2="0%" y2="100%">
      <stop offset="0%" style="stop-color:#faf9f5"/>
      <stop offset="100%" style="stop-color:#e8e6dc"/>
    </linearGradient>

    <!-- PATTERNS: grids overlay -->
    <pattern id="grid-light" width="40" height="40" patternUnits="userSpaceOnUse">
      <path d="M 40 0 L 0 0 0 40" fill="none" stroke="rgba(255,255,255,0.04)" stroke-width="1"/>
    </pattern>
    <pattern id="grid-dark" width="40" height="40" patternUnits="userSpaceOnUse">
      <path d="M 40 0 L 0 0 0 40" fill="none" stroke="rgba(0,0,0,0.03)" stroke-width="1"/>
    </pattern>
    <pattern id="dot-grid" width="20" height="20" patternUnits="userSpaceOnUse">
      <circle cx="10" cy="10" r="1" fill="rgba(0,0,0,0.06)"/>
    </pattern>

    <!-- ÍCONES reutilizáveis (uso: <use href="#icon-name">) -->
    <symbol id="icon-check" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
      <circle cx="12" cy="12" r="10"/><path d="M8 12l3 3 5-6"/>
    </symbol>
    <symbol id="icon-x" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
      <line x1="18" y1="6" x2="6" y2="18"/><line x1="6" y1="6" x2="18" y2="18"/>
    </symbol>
    <symbol id="icon-arrow-right" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
      <path d="M5 12h14M12 5l7 7-7 7"/>
    </symbol>
    <symbol id="icon-target" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
      <circle cx="12" cy="12" r="10"/><circle cx="12" cy="12" r="6"/><circle cx="12" cy="12" r="2"/>
    </symbol>
    <symbol id="icon-data" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
      <rect x="3" y="3" width="18" height="18" rx="2"/><path d="M3 9h18"/><path d="M9 21V9"/>
    </symbol>
    <symbol id="icon-brain" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
      <path d="M9.5 2A2.5 2.5 0 0 0 7 4.5v15a2.5 2.5 0 0 0 4.96.44 2.5 2.5 0 0 0 2.96-.08V4.5A2.5 2.5 0 0 0 9.5 2Z"/>
    </symbol>

  </defs>
</svg>
```

---

## 3. Templates de página

### 3.1 Capa dark (cover)

```html
<div class="a4-page">
  <svg class="page-svg" viewBox="0 0 794 1123" xmlns="http://www.w3.org/2000/svg">

    <!-- Background -->
    <rect width="794" height="1123" fill="url(#grad-dark)"/>
    <rect width="794" height="1123" fill="url(#grid-light)"/>
    <rect width="794" height="1123" fill="transparent" filter="url(#noise)" opacity="0.6"/>

    <!-- Header line -->
    <text x="60" y="80" font-family="'JetBrains Mono', monospace" fill="#d97757" font-size="13" letter-spacing="2">RELATÓRIO ESTRATÉGICO</text>
    <line x1="60" y1="98" x2="734" y2="98" stroke="rgba(255,255,255,0.15)" stroke-width="1"/>

    <!-- Display title -->
    <text x="60" y="380" font-family="'Playfair Display', serif" font-weight="900" fill="#ffffff" font-size="72" letter-spacing="-1">TÍTULO</text>
    <text x="60" y="460" font-family="'Poppins', sans-serif" font-weight="700" fill="transparent" stroke="#ffffff" stroke-width="1.5" font-size="72" letter-spacing="6">SUBTÍTULO</text>

    <!-- Accent bar -->
    <rect x="60" y="510" width="48" height="4" fill="#d97757"/>

    <!-- Tagline -->
    <text x="60" y="565" font-family="'Lora', serif" fill="#e0e5ec" font-size="22">Tagline da capa aqui</text>

    <!-- Info badge -->
    <rect x="60" y="620" width="260" height="90" fill="rgba(255,255,255,0.05)" stroke="rgba(255,255,255,0.1)" rx="4"/>
    <text x="80" y="657" font-family="'JetBrains Mono', monospace" fill="#d97757" font-size="13">DOCUMENTO #001</text>
    <text x="80" y="687" font-family="'Poppins', sans-serif" font-weight="700" fill="#ffffff" font-size="18">Nome do documento</text>

    <!-- Footer -->
    <line x1="60" y1="1023" x2="734" y2="1023" stroke="rgba(255,255,255,0.15)" stroke-width="1"/>
    <text x="60" y="1060" font-family="'JetBrains Mono', monospace" fill="#8898aa" font-size="11">ACESSO ABERTO • LEITURA: 3 MIN</text>
    <text x="734" y="1060" font-family="'JetBrains Mono', monospace" fill="#8898aa" font-size="11" text-anchor="end">PG. 01</text>
  </svg>
</div>
```

### 3.2 Página de conteúdo light (com sidebar)

```html
<div class="a4-page">
  <svg class="page-svg" viewBox="0 0 794 1123" xmlns="http://www.w3.org/2000/svg">

    <rect width="794" height="1123" fill="#f4f7fa"/>
    <rect width="794" height="1123" fill="url(#grid-dark)"/>

    <!-- Sidebar vertical -->
    <rect x="0" y="0" width="80" height="1123" fill="#1a365d"/>
    <text transform="rotate(-90, 40, 561)" x="40" y="561"
          font-family="'JetBrains Mono', monospace" fill="#ffffff" font-size="18"
          text-anchor="middle" letter-spacing="5">SEÇÃO</text>

    <!-- Content area começa em x=140 -->
    <text x="140" y="100" font-family="'JetBrains Mono', monospace" fill="#d97757" font-size="13">LABEL DE SEÇÃO</text>
    <text x="140" y="160" font-family="'Playfair Display', serif" font-weight="700" fill="#1a365d" font-size="44">Título da Seção</text>
    <line x1="140" y1="190" x2="734" y2="190" stroke="#cbd5e1" stroke-width="1"/>

    <!-- Body text -->
    <text x="140" y="240" font-family="'Lora', serif" fill="#334155" font-size="17">
      <tspan x="140" dy="0">Parágrafo de conteúdo principal vai aqui.</tspan>
      <tspan x="140" dy="32">Segunda linha do parágrafo.</tspan>
    </text>

    <!-- Info cards (3 colunas) -->
    <rect x="140" y="800" width="180" height="100" fill="#ffffff" stroke="#cbd5e1" rx="4"/>
    <rect x="140" y="800" width="180" height="4" fill="#6a9bcc"/>
    <text x="160" y="840" font-family="'Poppins', sans-serif" font-weight="700" fill="#1a365d" font-size="15">Card 1</text>
    <text x="160" y="868" font-family="'Lora', serif" fill="#64748b" font-size="12">Descrição</text>

    <rect x="340" y="800" width="180" height="100" fill="#ffffff" stroke="#cbd5e1" rx="4"/>
    <rect x="340" y="800" width="180" height="4" fill="#788c5d"/>
    <text x="360" y="840" font-family="'Poppins', sans-serif" font-weight="700" fill="#1a365d" font-size="15">Card 2</text>
    <text x="360" y="868" font-family="'Lora', serif" fill="#64748b" font-size="12">Descrição</text>

    <rect x="540" y="800" width="180" height="100" fill="#ffffff" stroke="#cbd5e1" rx="4"/>
    <rect x="540" y="800" width="180" height="4" fill="#d97757"/>
    <text x="560" y="840" font-family="'Poppins', sans-serif" font-weight="700" fill="#1a365d" font-size="15">Card 3</text>
    <text x="560" y="868" font-family="'Lora', serif" fill="#64748b" font-size="12">Descrição</text>

    <!-- Disclaimer / footer -->
    <text x="140" y="980" font-family="'JetBrains Mono', monospace" fill="#d97757" font-size="11" font-weight="700">⚠ AVISO LEGAL OU DISCLAIMER AQUI SE NECESSÁRIO</text>
    <text x="734" y="1060" font-family="'JetBrains Mono', monospace" fill="#8898aa" font-size="11" text-anchor="end">PG. 02</text>
  </svg>
</div>
```

---

## 4. Padrões SVG comuns

### Divider horizontal com label
```svg
<line x1="140" y1="400" x2="734" y2="400" stroke="#cbd5e1" stroke-width="1"/>
<rect x="140" y="392" width="120" height="16" fill="#f4f7fa"/>
<text x="150" y="404" font-family="'JetBrains Mono', monospace" fill="#94a3b8" font-size="10" letter-spacing="1">SEÇÃO 2</text>
```

### Callout box com left border
```svg
<rect x="140" y="440" width="594" height="100" fill="#ffffff" stroke="#1a365d" stroke-width="1.5" rx="4" filter="url(#shadow)"/>
<rect x="140" y="440" width="6" height="100" fill="#1a365d" rx="2"/>
<text x="170" y="488" font-family="'Poppins', sans-serif" font-weight="700" fill="#1a365d" font-size="18">Mensagem principal do callout aqui.</text>
<text x="170" y="516" font-family="'Lora', serif" fill="#64748b" font-size="14">Detalhe ou explicação adicional.</text>
```

### Item de checklist
```svg
<use href="#icon-check" x="140" y="560" width="28" height="28" stroke="#6a9bcc"/>
<text x="184" y="580" font-family="'Poppins', sans-serif" font-weight="700" fill="#1a365d" font-size="17">Item do checklist</text>
<text x="184" y="600" font-family="'Lora', serif" fill="#64748b" font-size="13">Descrição do item.</text>
```

### Progress bar / metric bar
```svg
<!-- Track -->
<rect x="140" y="700" width="594" height="20" fill="#e2e8f0" rx="3"/>
<!-- Fill (ajustar width pra %) -->
<rect x="140" y="700" width="475" height="20" fill="#1a365d" rx="3"/><!-- 80% -->
<!-- Label -->
<text x="625" y="715" font-family="'JetBrains Mono', monospace" fill="#1a365d" font-size="13" font-weight="700">80%</text>
```

### Elemento decorativo geométrico (neural/técnico)
```svg
<g transform="translate(600, 200)" stroke="rgba(0,0,0,0.06)" fill="none">
  <circle cx="0" cy="0" r="160" stroke-width="1" stroke-dasharray="4 8"/>
  <circle cx="0" cy="0" r="100" stroke-width="1"/>
  <circle cx="0" cy="0" r="40" stroke="#d97757" stroke-width="1.5" fill="none"/>
  <line x1="-180" y1="0" x2="180" y2="0" stroke-width="1"/>
  <line x1="0" y1="-180" x2="0" y2="180" stroke-width="1"/>
  <circle cx="70" cy="-70" r="5" fill="#6a9bcc" stroke="none"/>
  <circle cx="-50" cy="86" r="5" fill="#788c5d" stroke="none"/>
</g>
```

---

## 5. Catálogo de tipos de página

| Tipo | Background | Sidebar | Tipografia |
|---|---|---|---|
| Cover | Dark gradient + noise | Não | Display + Heading |
| Conteúdo light | `#f4f7fa` | Navy bar esquerda | Heading + Body |
| Conteúdo white | `#ffffff` | Sem ou top mono bar | Heading + Body |
| Dark section | Dark gradient + noise | Não | Heading branco + Body muted |
| CTA / final | Dark gradient | Não | Large heading + Mono |
| Data / charts | `#ffffff` | Opcional | Mono + Compact |
| Ethics / disclaimer | `#f4f7fa` | Não | Body + Callout boxes |

---

## 6. Print / Export — checklist

- [ ] `@media print` esconde body bg e remove page shadow
- [ ] `break-after: page` em `.a4-page`
- [ ] Pra PDF: Chrome → Print → Save as PDF → **"Background graphics" ON**
- [ ] Pra alta resolução: width/height em `mm` (browser renderiza no DPI da tela)
- [ ] Texto SVG renderiza como vetor (sem rasterização) — fontes precisam estar carregadas
- [ ] Testar com pelo menos 3 páginas pra validar break

---

## 7. Quando usar este engine vs PDF skill

| Cenário | Use |
|---|---|
| Documento A4 multi-página com layout visual rico (relatório executivo, manifesto, playbook) | **Este engine** (HTML+SVG, exporta via Print) |
| PDF gerado programaticamente com tabelas longas e dados dinâmicos | `/mnt/skills/public/pdf/SKILL.md` |
| PDF a partir de Markdown ou texto puro | `/mnt/skills/public/pdf/SKILL.md` |
| Form fillable PDF | `/mnt/skills/public/pdf/SKILL.md` |
| Documento com fluxos visuais, callouts, gráficos custom | **Este engine** |

Regra prática: se o documento for **mais visual que tabular**, use este engine. Se for o oposto, use a skill `pdf`.
