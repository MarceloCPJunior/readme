# ROTEIRO RESUMIDO - APRESENTAÇÃO RÁPIDA 3 MINUTOS
## Sistema de Integração Bancária e Análise de Fluxo Financeiro
## 11 Slides em 3 Minutos = ~16 segundos por slide

---

## ESTRATÉGIA DE TEMPO

**Problema identificado:** Você gastou 1min40 nos primeiros 3 slides
**Meta:** Distribuir 3 minutos em 11 slides de forma equilibrada
**Novo timing:** ~15-16 segundos por slide (máximo)

---

---

# SLIDE 1: TÍTULO [10 segundos]

"Bom dia/tarde. Sou Marcelo Junior, com Djalma Neto, orientados pelo Professor Marcelo.

Apresentamos um **sistema de gateway de pagamentos unificado** que integra múltiplos bancos 
com dashboard de gestão financeira e inteligência de dados."

**Tempo: 10 segundos**

---

# SLIDE 2: FUNDAMENTAÇÃO TEÓRICA [20 segundos]

"A solução usa **três pilares**: Microsserviços para módulos independentes, API Gateway 
como entrada única controlada, e Padrão de Adaptação - crucial porque cada banco tem 
protocolo diferente. O padrão encapsula cada banco em adaptador próprio, oferecendo 
interface normalizada. Novo banco? Apenas novo adaptador, sem mudar código existente."

**Tempo: 20 segundos**

---

# SLIDE 3: MÓDULO GATEWAY [12 segundos]

"Estruturamos em três módulos. O **Gateway** gerencia comunicação bancária com 
processamento seguro. Implementa retry automático, circuit breaker, e persistência 
que garante transações nunca perdidas."

**Tempo: 12 segundos**

---

# SLIDE 4: MÓDULO FINANCE [12 segundos]

"O **Finance** consolida dados dispersos em dashboards executivos. Oferece análise 
preditiva, projeções de fluxo de caixa, identifica tendências, calcula KPIs, e gera 
relatórios exportáveis."

**Tempo: 12 segundos**

---

# SLIDE 5: MÓDULO AUTH [12 segundos]

"O **Auth** garante segurança com autenticação centralizada JWT, controle de acesso 
granular, e auditoria completa de cada operação. Garante conformidade com LGPD e PCI-DSS."

**Tempo: 12 segundos**

---

# SLIDE 6: PADRÕES DE COMUNICAÇÃO [10 segundos]

"Módulos comunicam através de eventos assíncronos desacoplados. Orquestração coordena 
fluxos complexos. Segurança em múltiplas camadas protege dados."

**Tempo: 10 segundos**

---

# SLIDE 7: RESULTADO 1 - ABSTRAÇÃO [12 segundos]

"Resultados esperados: Primeiro, demonstrar abstração de APIs heterogêneas. Novo banco 
integrado sem impacto ao código - apenas novo adaptador. Escalabilidade exponencial."

**Tempo: 12 segundos**

---

# SLIDE 8: RESULTADO 2 - GATEWAY ROBUSTO [12 segundos]

"Segundo, gateway robusto e confiável. Transações nunca perdidas, nunca duplicadas. 
Auditoria completa. Confiabilidade apropriada para operações financeiras críticas."

**Tempo: 12 segundos**

---

# SLIDE 9: RESULTADO 3 - VISÃO CONSOLIDADA [12 segundos]

"Terceiro, dashboard unificado consolidando múltiplos bancos em uma tela. Visualizações 
intuitivas, relatórios exportáveis. Gestor entende saúde financeira em minutos."

**Tempo: 12 segundos**

---

# SLIDE 10: RESULTADO 4 - INTELIGÊNCIA [12 segundos]

"Quarto, inteligência financeira transformando dados em insights acionáveis. Projeções 
de fluxo futuro, alertas de anomalias, suporte à decisão estratégica."

**Tempo: 12 segundos**

---

# SLIDE 11: PRÓXIMOS PASSOS [40 segundos]

"Desenvolvimento em 6 fases, 24 sprints, 12 meses.

Fase 1: Fundações - infraestrutura e primeiro adaptador. 
Fase 2: Integração - múltiplos adaptadores e confiabilidade. 
Fase 3: Inteligência - agregação e projeções. 
Fase 4: Dashboard - frontend e visualizações. 
Fase 5: Segurança - auditoria e conformidade. 
Fase 6: Produção - otimização e 24/7.

Cada fase valida entregas concretas."

**Tempo: 40 segundos**

---

# CONCLUSÃO [8 segundos]

"Em resumo: sistema que unifica, simplifica e oferece inteligência para operações 
financeiras. Solução robusta, segura e escalável."

**Tempo: 8 segundos**

---

# AGRADECIMENTO [8 segundos]

"Agradecemos ao Professor Marcelo, à Coordenação, e à banca. Muito obrigado. 
Ficamos à disposição para perguntas."

**Tempo: 8 segundos**

---

---

## TIMING CONSOLIDADO - VERSÃO RÁPIDA

| Slide | Conteúdo | Tempo | Acumulado |
|-------|----------|-------|-----------|
| 1 | Título | 10s | 10s |
| 2 | Fundamentação | 20s | 30s |
| 3 | Gateway | 12s | 42s |
| 4 | Finance | 12s | 54s |
| 5 | Auth | 12s | 66s (1:06) |
| 6 | Padrões | 10s | 76s |
| 7 | Resultado 1 | 12s | 88s |
| 8 | Resultado 2 | 12s | 100s |
| 9 | Resultado 3 | 12s | 112s |
| 10 | Resultado 4 | 12s | 124s |
| 11 | Próximos Passos | 40s | 164s (2:44) |
| - | Conclusão | 8s | 172s |
| - | Agradecimento | 8s | 180s |
| **TOTAL** | | **180s** | **3:00 min** |

---

---

## ROTEIRO ULTRA-RESUMIDO (Versão Cola)

### SLIDE 1 [10s]
"Bom dia. Sou Marcelo Junior com Djalma Neto. Sistema de gateway bancário unificado com dashboard financeiro."

### SLIDE 2 [20s]
"Três pilares: Microsserviços, API Gateway, Padrão de Adaptação. Este último encapsula cada banco em adaptador - novo banco não muda código existente."

### SLIDE 3 [12s]
"Módulo Gateway gerencia comunicação bancária com retry, circuit breaker, persistência."

### SLIDE 4 [12s]
"Finance consolida dados em dashboards, análise preditiva, KPIs, relatórios."

### SLIDE 5 [12s]
"Auth oferece segurança JWT, controle de acesso, auditoria, conformidade LGPD."

### SLIDE 6 [10s]
"Comunicação por eventos, orquestração de fluxos, segurança em camadas."

### SLIDE 7 [12s]
"Resultado 1: Abstração de APIs. Novo banco sem impacto."

### SLIDE 8 [12s]
"Resultado 2: Gateway robusto. Transações nunca perdidas."

### SLIDE 9 [12s]
"Resultado 3: Dashboard unificado, múltiplos bancos em uma tela."

### SLIDE 10 [12s]
"Resultado 4: Inteligência financeira com projeções e alertas."

### SLIDE 11 [40s]
"6 fases, 24 sprints: Fundações, Integração, Inteligência, Dashboard, Segurança, Produção."

### CONCLUSÃO [8s]
"Sistema que unifica e simplifica operações financeiras."

### AGRADECIMENTO [8s]
"Obrigado ao Professor Marcelo, Coordenação e banca. Dúvidas?"

---

## TREINO RECOMENDADO

### Dia 1: Memorização
- Leia versão resumida 3-4 vezes em voz alta
- Cronometre cada slide
- Ajuste onde necessário

### Dia 2: Velocidade
- Pratique falando mais rápido
- Use cronômetro para cada slide
- Meta: não passar de tempo designado

### Dia 3: Naturalização
- Pratique sem ler
- Grave-se
- Assista e corrija

### Dia 4: Finalização
- Pratique apresentação completa 2-3 vezes
- Cronometre total
- Ajuste final

---

**IMPORTANTE:** Se perceber que está atrasado:

- **No slide 6:** Pule direto para "Comunicam por eventos"
- **Nos slides 7-10:** Diga apenas título do resultado (8s cada)
- **No slide 11:** Diga apenas "6 fases: Fundações, Integração, Inteligência, Dashboard, Segurança, Produção" (15s)
- Isso economiza ~1 minuto

Boa sorte! 🚀
