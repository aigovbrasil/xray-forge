# Brand Tokens — FORGE
## Fonte da verdade absoluta para cor, tipografia e forma

Este arquivo é referenciado por TODAS as outras camadas do skill.
Em caso de conflito entre este arquivo e qualquer outro, este vence.

---

## 1. Paleta

### Surfaces (texto e fundo)

| Token | Hex | Uso |
|---|---|---|
| `--forge-dark` | `#141413` | Texto primário em fundo claro · fundo dark mode |
| `--forge-light` | `#faf9f5` | Fundo light mode · texto sobre fundo dark |
| `--forge-mid-gray` | `#b0aea5` | Texto secundário · elementos muted · placeholder |
| `--forge-light-gray` | `#e8e6dc` | Fundos sutis · borders · dividers |

### Acentos (regra de ciclo)

Quando precisar de cor em múltiplos elementos, use **nesta ordem fixa**:

| Token | Hex | Uso semântico |
|---|---|---|
| `--forge-orange` | `#d97757` | **Primário** — CTAs, highlights, foco |
| `--forge-blue` | `#6a9bcc` | **Secundário** — links, info, dados |
| `--forge-green` | `#788c5d` | **Terciário** — success, tags, validação |

**Regra:** primeiro elemento colorido = orange. Segundo = blue. Terceiro = green. Não pular a ordem.

### Cores funcionais (estados)

Reservadas para feedback de sistema (não decoração):

```css
--success: #43A047;
--warning: #FF8F00;
--danger:  #ff6b6b;
--info:    #2196F3;
```

---

## 2. Tipografia

### Stack canônico

```css
--forge-heading: 'Poppins', Arial, sans-serif;
--forge-body:    'Lora', Georgia, serif;
--forge-mono:    'JetBrains Mono', 'SF Mono', Consolas, monospace;
```

**Carregamento via Google Fonts (sempre):**

```html
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Poppins:wght@400;500;700;800&family=Lora:ital,wght@0,400;0,500;0,700;1,400&family=JetBrains+Mono:wght@400;700&display=swap" rel="stylesheet">
```

### Quando usar cada uma

| Elemento | Família | Pesos permitidos |
|---|---|---|
| Headings ≥24px | Poppins | 700, 800 |
| Headings 14–23px | Poppins | 500, 700 |
| Body text 14–18px | Lora | 400 |
| Body emphasis | Lora | 500, 700 (`<strong>`) |
| Pull quotes editorial | Playfair Display (opcional, italic) | 700 |
| Labels uppercase | Poppins ou Mono | 500 |
| Code, números, dados tabulares | JetBrains Mono | 400, 700 |

### Regras de peso

- ✅ Permitidos: 400, 500, 700, 800
- ❌ Proibido: **600** (gera "AI slop" — sempre escolha 500 ou 700)
- Display extra-large (≥48px): apenas 800

### Tamanhos mínimos

- Texto legível: **mínimo 11px**
- Body padrão: 14–18px
- Line-height body: 1.55–1.7
- Letter-spacing labels uppercase: 0.06em

---

## 3. Shape rules

### Border radius

| Contexto | Valor |
|---|---|
| Default (botões pequenos, badges) | `4px` |
| Cards, inputs | `8px` |
| Cards grandes, painéis | `12px` |
| Modais, dialogs | `20px` |
| Pills, avatars circulares | `9999px` |

### Sombras

**Decorativo:** ❌ proibido

**Funcional permitido:**

```css
/* Cards elevados sobre fundo de página */
box-shadow: 0 8px 24px rgba(0,0,0,0.10);

/* Modais sobre overlay */
box-shadow: 0 32px 80px rgba(0,0,0,0.45);

/* Hover state em cards interativos */
box-shadow: 0 12px 32px rgba(0,0,0,0.14);
```

### Borders

```css
/* Default — light mode */
border: 1px solid rgba(0, 0, 0, 0.08);

/* Strong — para ênfase */
border: 1px solid rgba(0, 0, 0, 0.18);

/* Dark mode */
border: 1px solid rgba(255, 255, 255, 0.08);

/* Accent border (semântica) */
border-top: 4px solid var(--forge-orange);  /* card destacado */
border-left: 4px solid var(--forge-blue);   /* callout box */
```

---

## 4. Dark mode (obrigatório)

Todo artifact precisa passar este teste mental:
> "Se o fundo virasse near-black agora, todo texto ainda seria legível?"

### Padrão CSS variables (recomendado)

```css
:root {
  --bg: #faf9f5;
  --bg-surface: #ffffff;
  --text-primary: #141413;
  --text-secondary: #b0aea5;
  --border: rgba(0,0,0,0.08);
}

@media (prefers-color-scheme: dark) {
  :root {
    --bg: #1a1a18;
    --bg-surface: #232220;
    --text-primary: #faf9f5;
    --text-secondary: #b0aea5;
    --border: rgba(255,255,255,0.10);
  }
}

/* Uso */
body { background: var(--bg); color: var(--text-primary); }
.card { background: var(--bg-surface); border: 1px solid var(--border); }
```

### Padrão JS toggle (manual)

```js
const TOKEN_LIGHT = {
  '--bg': '#faf9f5', '--text-primary': '#141413', /*...*/
};
const TOKEN_DARK = {
  '--bg': '#1a1a18', '--text-primary': '#faf9f5', /*...*/
};

function applyTheme(theme) {
  const tokens = theme === 'dark' ? TOKEN_DARK : TOKEN_LIGHT;
  Object.entries(tokens).forEach(([k, v]) =>
    document.documentElement.style.setProperty(k, v));
}
```

---

## 5. Spacing scale (sistema de 4px)

```css
--space-1:  4px;
--space-2:  8px;
--space-3: 12px;
--space-4: 16px;
--space-5: 24px;
--space-6: 32px;
--space-7: 48px;
--space-8: 64px;
--space-9: 96px;
```

**Padding rítmico em containers:**
- Compacto: 12px / 16px
- Padrão: 20px / 24px
- Generoso: 32px / 48px

**Gap rítmico em flex/grid:**
- Compacto: 8px
- Padrão: 16px
- Generoso: 24px

---

## 6. Density modes (override de spacing)

Aplique via JS quando o usuário trocar densidade:

```js
const DENSITY_MODES = {
  executive: {
    '--density-gap': '24px',
    '--density-pad': '28px',
    '--table-row-h': '56px',
    '--text-base': '16px'
  },
  balanced: {
    '--density-gap': '16px',
    '--density-pad': '20px',
    '--table-row-h': '48px',
    '--text-base': '15px'
  },
  dense: {
    '--density-gap': '8px',
    '--density-pad': '12px',
    '--table-row-h': '36px',
    '--text-base': '13px'
  },
};
```

---

## 7. Anti-patterns (nunca fazer)

| Anti-pattern | Por quê | Substituto |
|---|---|---|
| Gradiente roxo de fundo | Default "AI slop" | Cor sólida da paleta |
| Inter font | Default "AI slop" | Poppins |
| Cantos arredondados em tudo | Sem hierarquia | Radius semântico (tabela acima) |
| Hex hardcoded `color: #333` | Quebra dark mode | `var(--text-primary)` |
| `font-weight: 600` | Look genérico | 500 ou 700 |
| Font-size 9–10px | Ilegível | Mínimo 11px |
| Drop shadow em ícone/badge | Decorativo gratuito | Sem sombra |
| Blur, glow, neon | "AI slop" | Flat surface |
| Emoji decorativo (🚀✨💡) | Genérico | SVG paths ou shapes |
| `position: fixed` em show_widget | Colapsa iframe | Layout flex/grid |
| `<html>/<head>/<body>` em show_widget | Quebra rendering | Apenas conteúdo |

---

## 8. Quick reference (cola na cabeça)

```
DARK   #141413   ← texto e bg dark
LIGHT  #faf9f5   ← bg e texto on dark
GRAY   #b0aea5   ← muted
LINE   #e8e6dc   ← borders sutis

ORANGE #d97757   ← 1º acento (CTA)
BLUE   #6a9bcc   ← 2º acento (info)
GREEN  #788c5d   ← 3º acento (success)

POPPINS  → headings
LORA     → body
JBM      → mono / dados

RADIUS   4 / 8 / 12 / 20 / 9999
WEIGHTS  400 · 500 · 700 · 800   (NUNCA 600)
```
