# CHANGELOG

Histórico de versões e relatório de auditoria do FORGE Visual Canvas.

---

## [2.0.0] — 2026-04-30 — Consolidação e empacotamento

Refator estrutural completo. Material espalhado em 7 documentos virou skill canônica empacotável.

### Auditoria do material v1 (input)

**Documentos brutos recebidos:**

| # | Arquivo | Conteúdo | Status v2 |
|---|---|---|---|
| 1 | `forge-brand.md` | Brand tokens (cores, fontes, shape rules) | ✅ Consolidado em `references/brand-tokens.md` |
| 2 | `FORGE_master_prompt.md` | Brand system + pipeline + clone reference | ✅ Mesclado no SKILL.md mestre + `brand-tokens.md` |
| 3 | `master-prompt.md` | Prompt parametrizável Visual Canvas Studio | ✅ Refinado em `assets/master-prompt-engine.md` |
| 4 | `visual-modes.md` | 10 linguagens visuais + 5 component systems | ✅ Separado em `references/visual-languages.md` + `references/component-systems.md` |
| 5 | `svg-document-engine.md` | PDFs A4 multi-página | ✅ Refinado em `references/svg-document-engine.md` (cores alinhadas com brand FORGE) |
| 6 | `claude_excel_modal_clone.html` | Gold standard de modal clone | ✅ Salvo em `assets/excel-modal-clone.html` com header explicativo |
| 7 | `conversa_que_gerou_Showroom_rex.md` | Conversa que gerou o Design Language Codex | ✅ Resumido em `examples/design-language-codex/README.md` |

### Gaps identificados no v1

| Gap | Severidade | Resolução v2 |
|---|---|---|
| Sem `SKILL.md` formal com YAML frontmatter | 🔴 crítico | Criado `SKILL.md` mestre com `name` + `description` "pushy" PT-BR/EN |
| Sem routing claro de "qual doc consultar quando" | 🔴 crítico | Decision tree no SKILL.md + linkagem entre arquivos |
| Sobreposição entre `master-prompt.md` e `FORGE_master_prompt.md` | 🟡 médio | Deduplicado: master prompt copy-paste em `assets/`, brand pipeline no SKILL.md |
| `visual-modes.md` misturava linguagens visuais e component systems | 🟡 médio | Separado em 2 arquivos com responsabilidade única |
| Sem matriz de combinação linguagem × componente | 🟢 baixo | Criada matriz em `references/component-systems.md` |
| Sem triggers em PT-BR (João opera em PT) | 🔴 crítico | `description:` agora prioriza phrasings PT-BR |
| `svg-document-engine.md` usava paleta inconsistente com brand FORGE | 🟡 médio | Cores acentos alinhadas: `#d97757` orange, `#6a9bcc` blue, `#788c5d` green |
| Sem slot pra extensão futura | 🟡 médio | Criado `extensions/` com README + 7 ideias de extensões backlog |
| Sem CHANGELOG | 🟢 baixo | Este arquivo |
| Sem README de instalação/uso | 🟡 médio | Criado `README.md` na raiz |
| Excel modal sem header explicativo | 🟢 baixo | Adicionado comentário HTML no topo explicando decisões e referências |
| Anti-patterns mencionados em 3 arquivos diferentes | 🟢 baixo | Consolidado numa seção única em `brand-tokens.md` |
| Lista de extensões instaladas vazia mas sem template | 🟢 baixo | Template completo em `extensions/README.md` |

### Mudanças de design intencionais

**Brand tokens centralizados.** Antes: paleta repetida (e às vezes divergente) em 4 arquivos. Agora: `brand-tokens.md` é fonte da verdade absoluta — vence em qualquer conflito.

**Description "pushy" pra triggar bem.** Conforme guideline da skill-creator, o Claude tem tendência a "undertriggar" skills. Description agora menciona explicitamente:
- Triggers PT-BR (operação principal do João)
- Triggers EN (compatibilidade com prompts copiados)
- Quando NÃO ativar (evita falso positivo em queries só-texto)

**Component systems separados de linguagens visuais.** São conceitos ortogonais — qualquer linguagem combina com qualquer sistema. Manter no mesmo arquivo confundia o Claude na hora de decidir.

**Padrão de extensão vs core.** Core (references/, assets/) é estável. Extensions é laboratório do João. Quando uma extensão amadurecer, é promovida ao core via novo CHANGELOG entry.

**Decision tree explícito no SKILL.md.** Antes: o Claude tinha que inferir qual formato usar. Agora: árvore de decisão clara mapeia tipo de pedido → formato de output.

### Princípios mantidos do v1

- Pipeline 3 camadas (estrutura → tokens → acabamento)
- 10 linguagens visuais catalogadas
- 5 sistemas de componentes
- Brand FORGE Anthropic-inspired (Poppins/Lora/JBM, paleta #141413/#faf9f5/#d97757/#6a9bcc/#788c5d)
- Anti-patterns explícitos (no Inter, no purple gradient, no weight 600)
- Master prompt template parametrizável (BUSINESS_CASE replaceable)

### Estrutura de saída v2

```
forge-visual-canvas/
├── SKILL.md                          (entry point, ~250 linhas)
├── README.md                         (overview, instalação)
├── CHANGELOG.md                      (este arquivo)
├── references/
│   ├── brand-tokens.md               (~280 linhas — fonte da verdade)
│   ├── visual-languages.md           (~290 linhas — 10 linguagens)
│   ├── component-systems.md          (~210 linhas — 5 sistemas + matriz)
│   └── svg-document-engine.md        (~330 linhas — PDFs A4)
├── assets/
│   ├── master-prompt-engine.md       (prompt copy-paste)
│   └── excel-modal-clone.html        (gold standard)
├── examples/
│   └── design-language-codex/
│       └── README.md                 (como regenerar)
└── extensions/
    ├── README.md                     (template + 7 ideias)
    └── .gitkeep
```

### Próximos passos sugeridos pra v2.1

1. **João adiciona primeira extensão** em `extensions/` — sugerido: `proposta-comercial-pme/` (alta utilidade pra rotina de consultoria presencial)
2. **Criar evals/** com 3-5 prompts de teste pra validar triggering
3. **Skill description optimizer** (rodar `run_loop.py` da skill-creator) — só faz sentido depois de ter casos reais de uso
4. **Tradução completa do prompt master** pra PT-BR (hoje está em EN porque o pipeline original era assim)
5. **Adicionar 11ª linguagem visual:** "Maia Consultoria" — paleta + fontes da marca pessoal do João, herdando estrutura mas com identidade própria

---

## [1.0.0] — antes de 2026-04-30 — Material bruto

Conjunto de documentos não-empacotados:
- forge-brand.md
- FORGE_master_prompt.md
- master-prompt.md
- visual-modes.md
- svg-document-engine.md
- claude_excel_modal_clone.html
- conversa_que_gerou_Showroom_rex.md

Funcional como referência pessoal, mas não acionável como skill (sem frontmatter, sem routing, sem triggers).
