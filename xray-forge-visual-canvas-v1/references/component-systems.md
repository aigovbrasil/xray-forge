# Component Systems — 5 Sistemas Catalogados

Component systems definem **como** as peças de UI são construídas — formato de botão, sombra de card, densidade de tabela, estilo de badge.

São **independentes** da linguagem visual. Você pode combinar, por exemplo, "Executive Swiss" (linguagem) com "shadcn/ui" (componentes).

---

## C1 — shadcn/ui Inspired (default)

Default recomendado. Cards arredondados, bordas finas, foco em conteúdo.

**Cards:**
```css
.card {
  background: var(--bg-surface);
  border: 0.5px solid var(--border);
  border-radius: var(--radius-lg);    /* 12px */
  padding: var(--density-pad);
  box-shadow: var(--shadow-sm);       /* 0 2px 8px rgba(0,0,0,0.06) */
}
```

**Botões:**
```css
.btn-primary {
  background: var(--text-primary);    /* preto/dark */
  color: var(--bg);                   /* claro */
  border: none;
  border-radius: var(--radius-md);    /* 8px */
  padding: 10px 20px;
  font-size: 14px;
  font-weight: 500;
}
.btn-ghost {
  background: transparent;
  border: 0.5px solid var(--border-strong);
  color: var(--text-primary);
  border-radius: var(--radius-md);
}
```

**Badges:**
- `border-radius: 9999px` (full pill)
- Texto pequeno
- Background: accent-soft (cor pastel)
- Texto: accent darkened
- Padding: 4px 10px

**Tabelas:**
- Border 0.5px só em rows (não em cells)
- Hover bg subtle
- Header com font-weight 500

**Combina bem com:** Executive Swiss, SaaS Premium, Apple Product, Linear/Vercel

---

## C2 — Tailwind Utility

Utility-first. Compor com tokens de spacing, sem abstrações de componente.

**Princípio:** classes utilitárias diretas, nada de `.card`/`.button`.

```html
<div class="bg-white rounded-lg border border-black/8 p-6 shadow-sm">
  <!-- conteúdo -->
</div>
```

**Botões:** transparentes + border em todos os 4 lados, sem radius decorativo (`rounded` apenas).

**Grid:**
```html
<div class="grid grid-cols-[repeat(auto-fit,minmax(200px,1fr))] gap-4">
  <!-- cards -->
</div>
```

**Quando usar:** prototipagem rápida, MVPs, projetos onde cada componente tem variação.

**Limitação no Claude artifacts:** apenas core utility classes do Tailwind funcionam (sem JIT compiler).

**Combina bem com:** SaaS Premium, Public Service, qualquer linguagem que não precise de componentes ricos.

---

## C3 — IBM Carbon Inspired

Estética enterprise: cantos duros, full-grid em tabelas, top-border colorido.

**Cards:**
```css
.carbon-card {
  border-top: 4px solid var(--accent-2);  /* azul Carbon */
  border: 1px solid var(--border-strong);
  border-radius: 0;                        /* SQUARE corners */
  padding: 16px;
  background: var(--bg-surface);
}
```

**Botões:**
- Flat
- **Square corners** (radius: 0)
- Full-width em mobile
- Primary: solid dark
- Secondary: outlined

```css
.carbon-btn {
  border-radius: 0;
  padding: 12px 24px;
  font-weight: 500;
  background: var(--text-primary);
  color: var(--bg);
  border: 2px solid transparent;
}
.carbon-btn-secondary {
  background: transparent;
  border: 2px solid var(--text-primary);
  color: var(--text-primary);
}
```

**Tabelas:** full grid border, alternating zebra rows, compact 36px row height.

**Notification:** left border 4px + ícone + texto. Cores funcionais (blue/green/yellow/red).

**Combina bem com:** Enterprise Dashboard, Bloomberg Terminal, Public Service.

---

## C4 — Material Design Inspired

Sistema de elevação por sombra. FABs, chips circulares, ripple effects.

**Sistema de elevação:**
```css
.material-1 { box-shadow: 0 1px 3px rgba(0,0,0,0.12),
                          0 1px 2px rgba(0,0,0,0.24); }
.material-2 { box-shadow: 0 3px 6px rgba(0,0,0,0.16),
                          0 3px 6px rgba(0,0,0,0.23); }
.material-3 { box-shadow: 0 10px 20px rgba(0,0,0,0.19),
                          0 6px 6px rgba(0,0,0,0.23); }
.material-4 { box-shadow: 0 14px 28px rgba(0,0,0,0.25),
                          0 10px 10px rgba(0,0,0,0.22); }
.material-5 { box-shadow: 0 19px 38px rgba(0,0,0,0.30),
                          0 15px 12px rgba(0,0,0,0.22); }
```

**FAB:** 56px circle, accent color, ícone centralizado, shadow-3.

**Chips:** 32px height, padding 16px horizontal, radius full, outlined ou filled.

**Ripple effect:**
```css
@keyframes ripple {
  to {
    transform: scale(4);
    opacity: 0;
  }
}
.ripple {
  position: absolute;
  border-radius: 50%;
  background: rgba(255,255,255,0.4);
  animation: ripple 600ms linear;
}
```
JS adiciona/remove `.ripple` no click.

**Combina bem com:** Material Design (linguagem), apps Android-style.

---

## C5 — Ant Design Inspired

Tabelas compactas, tags coloridas, formulários com label-acima.

**Tabelas:**
- Compact mode 40px rows
- Header bg `#FAFAFA`
- Border `#F0F0F0`

**Tags/Status chips:**
```css
.antd-tag {
  display: inline-flex;
  align-items: center;
  padding: 0 8px;
  height: 22px;
  font-size: 12px;
  border-radius: 4px;        /* não pill */
  border: 1px solid currentColor;
}
.antd-tag.success { color: #52c41a; background: #f6ffed; border-color: #b7eb8f; }
.antd-tag.warning { color: #fa8c16; background: #fff7e6; border-color: #ffd591; }
.antd-tag.danger  { color: #ff4d4f; background: #fff1f0; border-color: #ffa39e; }
.antd-tag.info    { color: #1890ff; background: #e6f7ff; border-color: #91d5ff; }
```

**Formulários:** label acima do input, height 40px, validation state colors abaixo.

**Pagination:** numerada compacta, prev/next com setas, estilo borderless.

**Combina bem com:** Enterprise Dashboard, sistemas internos ricos em formulários.

---

## Matriz de combinação

| Linguagem visual | shadcn/ui | Tailwind | Carbon | Material | Ant |
|---|:-:|:-:|:-:|:-:|:-:|
| Executive Swiss | ✅ ideal | ⚠️ ok | ✅ ideal | ❌ overkill | ⚠️ ok |
| SaaS Premium | ✅ ideal | ✅ ideal | ❌ frio | ❌ datado | ❌ datado |
| Enterprise Dashboard | ⚠️ ok | ⚠️ ok | ✅ ideal | ⚠️ ok | ✅ ideal |
| Public Service | ⚠️ ok | ✅ ideal | ⚠️ ok | ❌ não-acessível | ❌ não-acessível |
| Editorial Premium | ❌ excessivo | ✅ ideal (custom) | ❌ não combina | ❌ não combina | ❌ não combina |
| McKinsey | ✅ ideal | ⚠️ ok | ✅ ideal | ❌ overkill | ❌ visual conflitante |
| Bloomberg Terminal | ❌ não combina | ⚠️ ok | ✅ ideal | ❌ não combina | ⚠️ ok |
| Apple Product | ✅ ideal | ✅ ideal | ❌ rígido | ⚠️ ok | ❌ não combina |
| Material Design | ⚠️ ok | ⚠️ ok | ❌ não combina | ✅ ideal | ❌ visual conflitante |
| Linear/Vercel | ✅ ideal | ✅ ideal | ❌ rígido | ❌ não combina | ❌ não combina |

**Regra prática:** se em dúvida, escolha **shadcn/ui**. Funciona em 80% dos casos.

---

## Density modes (transversal a todos os sistemas)

Ver `brand-tokens.md` seção 6 — apply via JS ao trocar selector de densidade.
