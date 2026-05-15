# Visual Languages — Catálogo das 10 Linguagens

Cada linguagem é um sistema estético completo: paleta, tipografia, densidade, lógica de layout e tom.
Carregue este arquivo quando precisar de specs além do quick-select da SKILL.md mestre.

**Importante:** linguagens herdam os tokens base de `brand-tokens.md`. Os overrides aqui são *deltas*, não substituições totais.

---

## Quick select

| # | Linguagem | Quando usar |
|---|---|---|
| 1 | Executive Swiss | Relatórios C-level, propostas, diagnósticos B2B |
| 2 | SaaS Premium | Landing pages, produtos AI-first, MVPs |
| 3 | Enterprise Dashboard | Painéis ops, BI, monitoramento dense |
| 4 | Public Service | Formulários, onboarding, fluxos consultivos |
| 5 | Editorial Premium | Manifestos, whitepapers, autoridade |
| 6 | McKinsey Consulting | Due diligence, board presentations, M&A |
| 7 | Bloomberg Terminal | Trading dashboards, cockpit financeiro |
| 8 | Apple Product | Apps consumer, onboarding premium |
| 9 | Material Design | Apps Android, sistemas com elevação |
| 10 | Linear/Vercel | Dev tools, ferramentas técnicas modernas |

---

## 1. Executive Swiss
*Swiss Design + McKinsey Executive Consulting*

**Quando:** relatórios, PDFs, propostas, diagnósticos, business cases, apresentações C-level, decks B2B.

**Paleta:**
```
Navy primary:   #1A2744
Slate:          #2E3F5C
Accent blue:    #2563EB
Accent soft:    #DBEAFE
Charcoal:       #374151
Mid gray:       #6B7280
Light gray:     #F3F4F6
Border:         #D1D5DB
White:          #FFFFFF
```

**Tipografia:**
- Headings: Poppins/Montserrat 700/800, tracking apertado
- Body: Lora/Merriweather 400, line-height 1.7
- Labels/mono: JetBrains Mono
- Sem fontes decorativas

**Layout:**
- Grid 12 colunas estrito
- Whitespace generoso (margens ≥60px)
- Dividers finos horizontais (1px, #D1D5DB)
- Headings analíticos ("Estrutura de Liderança" não "Nosso Time")
- Sidebar com accent bar (4px navy à esquerda)
- Insight boxes com top border navy
- Page numbers em mono no footer

**Prompt trigger:**
> "Use Executive Swiss style: Swiss grid discipline, McKinsey executive consulting aesthetics. Whitespace generoso, headings Poppins, body Lora, paleta navy/slate, informação densa porém legível, dividers finos, headings analíticos, feel de documento C-level."

---

## 2. SaaS Premium
*Stripe + Linear + Vercel*

**Quando:** landing pages, product pages, AI-first interfaces, MVPs, marketing SaaS, waitlists.

**Paleta light:**
```
BG:           #FAFAFA
Surface:      #FFFFFF
Border:       rgba(0,0,0,0.08)
Text:         #111111
Muted:        #6B6B6B
Accent:       #0070F3   (Vercel blue) ou #635BFF (Stripe purple)
Accent soft:  #EEF2FF
```

**Paleta dark:**
```
BG:           #0A0A0A
Surface:      #111111
Border:       rgba(255,255,255,0.08)
Text:         #EDEDED
Muted:        #888888
Accent:       #0070F3
```

**Tipografia:**
- System font stack OU Inter (aceitável aqui — contexto produto)
- Hero type: 48–80px, weight 700
- Gradient text permitido apenas no hero
- Mono pra code snippets, decimais de pricing

**Layout:**
- Cards: `border: 1px solid rgba(0,0,0,0.08)`, radius 12px
- Padding generoso (24–48px)
- Section-based scrolling
- Feature grids: 3 colunas, ícone + título + descrição
- Decoração mínima — whitespace faz o trabalho
- Gradient sutil de fundo permitido apenas no hero

**Prompt trigger:**
> "Use SaaS Premium: inspiração Stripe + Linear + Vercel. Feel moderno de produto SaaS, cards limpos, profundidade sutil, bordas finas, tipografia crisp, seções modulares, spacing polido, estética premium AI-startup."

---

## 3. Enterprise Dashboard
*IBM Carbon + Microsoft Fluent + Bloomberg*

**Quando:** painéis ops, dashboards de métricas, BI tools, sistemas internos, monitoring, B2B data-heavy.

**Paleta:**
```
BG:           #F3F4F6
Surface:      #FFFFFF
Surface-2:    #F9FAFB
Border:       #E5E7EB
Text:         #111827
Muted:        #6B7280
Accent blue:  #2563EB
Accent soft:  #DBEAFE
Success:      #059669
Warning:      #D97706
Danger:       #DC2626
```

**Tipografia:**
- Sans compacta: IBM Plex Sans, Roboto, ou system UI
- Tamanhos pequenos OK (12–14px pra dados densos)
- Mono para todos números, métricas, codes
- ZERO serif — puramente funcional

**Layout:**
- Grid denso: base 8px
- Linhas de tabela compactas (36–40px height)
- Status chips/badges em todo lugar
- Sidebar navigation padrão
- Card headers com top border colorido (4px)
- Métricas em grids 2×2 ou 4×1
- Horizontal rules entre seções

**Prompt trigger:**
> "Use Enterprise Dashboard: inspiração IBM Carbon + Bloomberg + Microsoft Fluent. Painéis operacionais densos, tabelas limpas, layout metrics-first, paleta neutra cinza, acentos azul, componentes de dashboard, clareza B2B técnica, alta densidade informacional."

---

## 4. Public Service
*GOV.UK Design System*

**Quando:** formulários, onboarding flows, questionários, diagnósticos consultivos, processos user-facing.

**Paleta:**
```
BG:           #FFFFFF
Surface:      #F3F4F6
Text:         #0B0C0C
Muted:        #505A5F
Accent:       #1D70B8
Accent focus: #FFD600 (focus ring — acessibilidade)
Success:      #00703C
Warning:      #F47738
Danger:       #D4351C
Border:       #B1B4B6
```

**Tipografia:**
- GDS Transport ou Arial — proibido qualquer fonte decorativa
- Labels grandes (18–20px) com contraste forte
- Error messages em vermelho com ícone
- Helper text muted abaixo dos campos

**Layout:**
- Largura máxima 840px (line length legível)
- Formulários single-column — nunca lado a lado
- Step indicators claros ("Passo X de Y")
- Click targets grandes (mínimo 44px)
- Sem borders em cards — seções usam só vertical spacing
- Focus rings: amarelo grosso (#FFD600)
- Sem imagens decorativas, sem ilustrações

**Prompt trigger:**
> "Use Public Service style: inspirado GOV.UK service design. Alta acessibilidade, linguagem simples, alto contraste, estrutura de formulário simples, labels claros, hierarquia step-by-step, baixa carga cognitiva, task-oriented pra usuários não-técnicos."

---

## 5. Editorial Premium
*Whitepaper + Magazine + Thought Leadership*

**Quando:** manifestos, whitepapers, conteúdo de autoridade, narrative strategy docs, brand stories.

**Paleta:**
```
BG:           #FAF9F5    (off-white aquecido — light mode FORGE)
Surface:      #FFFFFF
Text:         #1A1A1A
Muted:        #6B6B6B
Pull quote:   #141413
Accent:       #D97757    (laranja FORGE)
Border:       #E8E6DC
```

**Tipografia:**
- Display: Playfair Display 700/900 — chapter titles
- Subheadings: Poppins/Montserrat 600
- Body: Lora/Merriweather 400 a 18–20px, line-height 1.8
- Pull quotes: Playfair italic, 24–32px
- Captions: Poppins 400, 12px, muted

**Layout:**
- Margens externas largas (80–100px de cada lado)
- Pull quotes centralizadas com linhas decorativas
- Chapter numbers em type grande muted (opacity 0.08)
- Section breaks: rule fina + 48px de espaço
- Primeiro parágrafo após heading: drop cap ou small-caps
- Column splits só pra conteúdo comparativo
- Sem badges, chips, componentes UI — pura editorial

**Prompt trigger:**
> "Use Editorial Premium: layout magazine + whitepaper. Tipografia elegante, Playfair Display em display heads, Lora body, margens generosas, pull quotes, contraste serif/sans, spacing refinado, estrutura narrativa, estética premium de autoridade."

---

## 6. McKinsey Consulting (Extended)
*Pure Strategy Consulting*

**Quando:** due diligence, recomendações estratégicas, board presentations, materiais M&A.

Essencialmente Executive Swiss com **densidade informacional maior** e **framing "so what" explícito**.

Regras adicionais:
- Todo heading **declara a conclusão**, não o tópico
  - ❌ "Análise de mercado"
  - ✅ "Mercado contrai 12% — entrada via partnership é defensável"
- Todo gráfico tem **insight box acima** dizendo o que o dado significa
- **Mekko / waterfall charts** preferidos sobre pie charts
- Estrita: **uma key message por slide/seção**
- Footer com page number + título do projeto + cliente em mono

---

## 7. Bloomberg Terminal (Extended)
*Maximum Data Density*

**Quando:** trading dashboards, financial data cockpits, monitoring panels, real-time ops.

**Paleta:**
```
BG:           #1C2127 (very dark blue-gray)
Surface:      #262D35
Border:       #373E47
Text:         #E6EDF3
Muted:        #848D97
Green (up):   #3FB950
Red (down):   #F85149
Blue (data):  #58A6FF
Yellow (warn):#D29922
```

**Regras:**
- Sem cantos arredondados — tudo retângulo
- Sem sombras
- Font: mono only
- Tabular figures everywhere
- Linhas de tabela com height 24–28px (max densidade)
- Cores semânticas estritas: verde sobe, vermelho desce, azul é dado

---

## 8. Apple Product (Extended)
*Consumer Product Premium*

**Quando:** consumer apps, lifestyle products, premium onboarding, brand experiences.

**Regras:**
- SF Pro ou system font apenas
- Background: branco puro OU preto puro (sem off-white)
- **Um** accent color máximo
- Padding generoso (60–80px em seções)
- Ícones: SF Symbols style (thin, stroke 1–1.5px)
- Sem ilustrações — fotos ou nada

---

## 9. Material Design (Extended)
*Google Material 3*

**Quando:** apps Android, sistemas web com elevação visual, dashboards orientados a card.

**Paleta:**
```
Primary:     #6750A4 (Material default purple — substituível)
Surface:     #FFFBFE
On surface:  #1C1B1F
Outline:     #79747E
Container:   #E8DEF8
```

**Regras:**
- Elevation system (5 níveis de sombra escalonada)
- FAB (floating action button) circular 56px
- Chips 32px com radius full
- Ripple effect em interações
- Headlines: Roboto Flex ou Roboto

---

## 10. Linear / Vercel (Extended)
*Developer Tooling Premium*

**Quando:** dev tools, ferramentas técnicas, terminais web, IDE-like UIs.

**Paleta dark (default):**
```
BG:           #08090A
Surface:      #101113
Border:       #1F2024
Text:         #E5E5E6
Muted:        #8A8A8E
Accent:       #5E6AD2 (Linear purple-blue)
```

**Regras:**
- Geist Sans (Vercel) ou Inter como exceção justificada
- Cantos sutis (radius 6px)
- Animações snappy (transition 100–150ms)
- Keyboard-first feel: shortcuts visíveis, command palette presente
- Densidade média (não dense terminal, não generosa SaaS)

---

## Como combinar Linguagem × Sistema de Componentes

Ver matriz completa em `component-systems.md`.

Combinações recomendadas (resumo):

| Linguagem visual | Componente recomendado | Razão |
|---|---|---|
| Executive Swiss | shadcn/ui ou Carbon | Cards limpos + tabelas estruturadas |
| SaaS Premium | shadcn/ui ou Tailwind | Modular, composable |
| Enterprise Dashboard | Carbon ou Ant Design | Tabelas densas, status chips |
| Editorial Premium | Custom (sem lib) | Editorial não tem componentes — só layout |
| Public Service | Tailwind ou GOV.UK custom | Acessibilidade + estrutura plain |
| Bloomberg Terminal | Carbon | Ambos densos e funcionais |
| Apple Product | shadcn/ui | Ambos minimal e polidos |
| Material Design | Material UI ou MD3 nativo | Sistema próprio |
| Linear/Vercel | shadcn/ui | Match natural |
| McKinsey | shadcn/ui ou Carbon | Mesma lógica do Executive Swiss |
