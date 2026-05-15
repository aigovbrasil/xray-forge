# FORGE Master Prompt Engine
## Copy → Paste → Replace [BUSINESS_CASE] → Generate

Este prompt gera um **artifact de canvas visual** onde o conteúdo é fixo
(definido em BUSINESS_CASE) mas o design language é trocável em runtime
via control panel (4 selectors: style / component / density / theme).

---

## Como usar

1. Copie todo o bloco "PROMPT INTEIRO" abaixo
2. Substitua o bloco `BUSINESS_CASE` pelo seu conteúdo
3. Cole no Claude
4. Receba: single-file HTML com selectors funcionais + calculator + SVG charts

---

## PROMPT INTEIRO (copy-paste)

```
You are FORGE, a principal-level full-stack AI product engineer and premium frontend designer.

Your task is to generate a single self-contained interactive business artifact using
the FORGE Visual Canvas Studio architecture described below.

The artifact works like a reusable visual canvas:
- Business content is fixed (defined in BUSINESS_CASE below)
- Visual design language is switchable via selector
- Component system is switchable via selector
- Density and theme are switchable via selector
- All style changes apply immediately without page reload
- Charts are native SVG — no external chart libraries
- The result must feel strategy-grade, not a generic dashboard

---

## BUSINESS_CASE

[REPLACE THIS ENTIRE BLOCK WITH YOUR CONTENT]

Name: AI Workflow Skill Studio
Tagline: Custom AI skills for consultants and micro-agencies
Target: Brazilian independent consultants, micro-agencies, B2B service providers
Core offer: 48-hour custom AI skill package — R$297 validation price
Expansion: Skill packs → Monthly maintenance → Industry kits → White-label → Enterprise
Goal: Validate fast, sell manually, identify strongest willingness-to-pay workflow category

Key numbers (for calculator defaults):
- Price per unit: R$297
- Target monthly sales: 10
- Delivery hours per project: 8
- Hourly operational cost: R$80
- Retainer conversion rate: 20%

Segments:
- Independent consultants (pain: high, budget: medium, AI maturity: medium)
- Micro agencies (pain: high, budget: medium-high, AI maturity: high)
- Accountants/legal (pain: medium, budget: medium, AI maturity: low)
- B2B service founders (pain: very high, budget: high, AI maturity: medium)

Channels (speed/trust/cost/conversion):
- WhatsApp: fast/high/low/high
- LinkedIn: slow/medium/medium/medium
- Referrals: medium/very high/zero/very high
- Community posts: fast/medium/zero/medium
- Cold email: slow/low/low/low
- Partnerships: slow/high/medium/high

Risk register:
- Overengineering: technical/high prob/high impact
- Weak ICP: strategic/medium/high
- Generic positioning: marketing/high/medium
- Excess delivery time: operational/medium/high
- Low perceived value: commercial/medium/high

6-week roadmap:
- W1: Manual validation (WhatsApp outreach, 3 sales)
- W2: Delivery standardization (template creation)
- W3: First reusable skill templates
- W4: Niche selection based on W1–3 data
- W5: Retainer test with first clients
- W6: Productized offer documentation

---

## REQUIRED SECTIONS

Build all of these as interactive tabs/sections:

1. Overview — Strategic summary card, value prop, monetization thesis, who pays, why now
2. Canvas — 9-block Business Model Canvas (visual grid)
3. ICP Matrix — Comparison table: 4 segments × 6 axes (pain/budget/AI maturity/friction/priority)
4. Offer Ladder — Pricing table: 5 tiers with price/format/trigger/complexity/margin/priority
5. Market Logic — SVG visual diagram explaining the "why now"
6. Channels — SVG bar chart comparing 6 acquisition channels across 5 dimensions
7. Economics — Live JS calculator with real-time margin calculation
8. Roadmap — 6-week timeline SVG + milestone table
9. Risks — Risk register table with probability/impact matrix
10. Decision — GO / REFINE / STOP panel with criteria

---

## VISUAL SYSTEM (FORGE Brand Tokens)

### Token architecture (CSS variables — apply to :root)

:root {
  --bg: #faf9f5; --bg-surface: #ffffff; --bg-elevated: #ffffff; --bg-subtle: #e8e6dc;
  --text-primary: #141413; --text-secondary: #b0aea5; --text-on-dark: #faf9f5;
  --border: rgba(0,0,0,0.08); --border-strong: rgba(0,0,0,0.18);
  --accent: #d97757; --accent-soft: #f5ddd5;
  --accent-2: #6a9bcc; --accent-2-soft: #d6e8f5;
  --accent-3: #788c5d;
  --success: #43A047; --warning: #FF8F00; --danger: #ff6b6b; --info: #2196F3;
  --font-heading: 'Poppins', Arial, sans-serif;
  --font-body: 'Lora', Georgia, serif;
  --font-mono: 'JetBrains Mono', 'SF Mono', Consolas, monospace;
  --radius-sm: 4px; --radius-md: 8px; --radius-lg: 12px; --radius-xl: 20px;
  --shadow-sm: 0 2px 8px rgba(0,0,0,0.06); --shadow-md: 0 8px 24px rgba(0,0,0,0.10);
  --density-gap: 16px; --density-pad: 20px; --table-row-h: 48px;
}

### Style mode overrides (apply via JS when selector changes)

const STYLE_MODES = {
  'executive-swiss': {
    '--bg':'#f4f7fa','--bg-surface':'#ffffff','--text-primary':'#0a1526',
    '--text-secondary':'#64748b','--accent':'#1a365d','--accent-soft':'#dbeafe',
    '--accent-2':'#2196F3','--font-heading':"'Poppins', sans-serif",
    '--font-body':"'Lora', serif",'--radius-md':'4px'
  },
  'saas-premium': {
    '--bg':'#0f0f0f','--bg-surface':'#1a1a1a','--text-primary':'#f0f0f0',
    '--text-secondary':'#888','--accent':'#d97757','--radius-md':'12px',
    '--border':'rgba(255,255,255,0.08)'
  },
  'enterprise-dashboard': {
    '--bg':'#f3f4f6','--bg-surface':'#ffffff','--text-primary':'#111827',
    '--text-secondary':'#6B7280','--accent':'#2563EB','--accent-soft':'#DBEAFE',
    '--radius-md':'4px','--density-gap':'8px','--density-pad':'12px','--table-row-h':'36px'
  },
  'public-service': {
    '--bg':'#ffffff','--bg-surface':'#f3f4f6','--text-primary':'#0b0c0c',
    '--accent':'#1d70b8','--radius-md':'0px','--radius-lg':'0px'
  },
  'editorial-premium': {
    '--bg':'#faf9f5','--bg-surface':'#ffffff','--text-primary':'#1a1a1a',
    '--accent':'#d97757','--font-heading':"'Playfair Display', Georgia, serif",
    '--font-body':"'Lora', serif",'--radius-md':'2px','--shadow-md':'none'
  }
};

### Density modes

const DENSITY_MODES = {
  'executive': { '--density-gap':'24px','--density-pad':'28px','--table-row-h':'56px' },
  'balanced':  { '--density-gap':'16px','--density-pad':'20px','--table-row-h':'48px' },
  'dense':     { '--density-gap':'8px', '--density-pad':'12px','--table-row-h':'36px' }
};

---

## CONTROL PANEL UI

Render a floating control panel (top of page or sidebar):

<div id="forge-controls">
  <label>Visual Language
    <select id="style-select">
      <option value="executive-swiss" selected>Executive Swiss</option>
      <option value="saas-premium">SaaS Premium</option>
      <option value="enterprise-dashboard">Enterprise Dashboard</option>
      <option value="public-service">Public Service</option>
      <option value="editorial-premium">Editorial Premium</option>
    </select>
  </label>

  <label>Component System
    <select id="component-select">
      <option value="shadcn" selected>shadcn/ui Inspired</option>
      <option value="carbon">IBM Carbon</option>
      <option value="material">Material Design</option>
      <option value="antd">Ant Design</option>
    </select>
  </label>

  <label>Density
    <select id="density-select">
      <option value="balanced" selected>Balanced</option>
      <option value="executive">Executive</option>
      <option value="dense">Dense</option>
    </select>
  </label>

  <label>Theme
    <select id="theme-select">
      <option value="light" selected>Light</option>
      <option value="dark">Dark</option>
    </select>
  </label>
</div>

Bind all selectors:

function applyTokens(overrides) {
  Object.entries(overrides).forEach(([k, v]) =>
    document.documentElement.style.setProperty(k, v));
}
document.getElementById('style-select').addEventListener('change', e =>
  applyTokens(STYLE_MODES[e.target.value] || {}));
document.getElementById('density-select').addEventListener('change', e =>
  applyTokens(DENSITY_MODES[e.target.value] || {}));

---

## UNIT ECONOMICS CALCULATOR

<div id="calc-section">
  <label>Price per skill (R$) <input type="number" id="price" value="297"/></label>
  <label>Monthly sales <input type="number" id="sales" value="10"/></label>
  <label>Delivery hours/project <input type="number" id="hours" value="8"/></label>
  <label>Hourly cost (R$) <input type="number" id="hcost" value="80"/></label>
  <label>Retainer conversion % <input type="number" id="ret" value="20"/></label>

  <div id="revenue">Monthly Revenue: R$ —</div>
  <div id="cost">Delivery Cost: R$ —</div>
  <div id="margin">Gross Margin: — %</div>
  <div id="mrr">Retainer MRR: R$ —</div>
  <div id="breakeven">Break-even signal: —</div>
</div>

<script>
function calc() {
  const p=+document.getElementById('price').value,
        s=+document.getElementById('sales').value,
        h=+document.getElementById('hours').value,
        hc=+document.getElementById('hcost').value,
        r=+document.getElementById('ret').value/100;
  const revenue=p*s, cost=h*hc*s, margin=revenue>0?((revenue-cost)/revenue*100):0;
  const retainerVal=p*0.3;
  const mrr=Math.round(s*r*retainerVal);
  document.getElementById('revenue').textContent=`Monthly Revenue: R$ ${revenue.toLocaleString('pt-BR')}`;
  document.getElementById('cost').textContent=`Delivery Cost: R$ ${cost.toLocaleString('pt-BR')}`;
  document.getElementById('margin').textContent=`Gross Margin: ${margin.toFixed(1)}%`;
  document.getElementById('mrr').textContent=`Retainer MRR: R$ ${mrr.toLocaleString('pt-BR')}`;
  document.getElementById('breakeven').textContent=margin>50?'✓ Healthy':'⚠ Review pricing';
}
['price','sales','hours','hcost','ret'].forEach(id =>
  document.getElementById(id).addEventListener('input', calc));
calc();
</script>

---

## OUTPUT INSTRUCTIONS

1. Generate a single self-contained HTML file (no build tools, no external libs except Google Fonts)
2. Include ALL 10 sections as tabs or scroll sections
3. Implement ALL 4 selectors with immediate token application
4. Include live unit economics calculator with real numbers
5. Include at least 3 native SVG charts (channel bars, roadmap timeline, market logic)
6. Apply Executive Swiss as default visual mode
7. Apply shadcn/ui Inspired as default component system
8. Apply Balanced density as default
9. Apply Light theme as default
10. Footer: "FORGE Visual Canvas Studio — same logic, variable visual system"
11. Token preview strip in footer showing active color, font, radius, density values

---

## QUALITY CHECKLIST (verify before output)

- [ ] No external chart libraries
- [ ] No lorem ipsum — all real business content from BUSINESS_CASE
- [ ] Token system applied — CSS variables throughout, no hardcoded hex
- [ ] Style switcher updates DOM immediately
- [ ] Calculator shows real computed numbers
- [ ] At least 3 native SVG charts
- [ ] Poppins for headings, Lora for body
- [ ] Dark mode toggle works
- [ ] Artifact looks strategy-grade — not a generic admin panel
- [ ] All 10 sections present
- [ ] No font-weight 600 anywhere
- [ ] No purple gradient backgrounds
- [ ] No Inter font

GENERATE THE ARTIFACT NOW.
```

---

## Como reusar este prompt

Para gerar um artifact pra outro contexto:
1. Substitua o bloco BUSINESS_CASE por novo conteúdo
2. Mantenha as seções de visual system, token, component e control panel intactas
3. Ajuste defaults do calculator pros números do novo caso
4. Cole o prompt completo no Claude

Para mudar a linguagem visual default:
- Mude o `selected` no `<option>` do `style-select`
- Mude qual chave do `STYLE_MODES` é aplicada na chamada inicial de `applyTokens()`

Para adicionar uma linguagem visual nova:
- Adicione entrada em `STYLE_MODES` com CSS variable overrides
- Adicione `<option>` no dropdown `style-select`
- Consulte `references/visual-languages.md` pra paleta e tipografia

---

## Variantes do prompt (slots pra extensão)

Conforme você desenvolver casos de uso novos, salve variantes em `extensions/<seu-caso>/master-prompt.md` mantendo a mesma estrutura.

Exemplos de variantes futuras:
- `extensions/proposta-comercial/` — sections diferentes (Hero, Problema, Solução, Pricing, FAQ, Termos)
- `extensions/diagnostico-pme/` — sections (Inputs do cliente, Análise, Plano de ação, Próximos passos)
- `extensions/playbook-operacional/` — sections (Visão, SOPs, Métricas, Riscos, Owners)
