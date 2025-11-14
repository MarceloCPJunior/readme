# ROTEIRO RESUMIDO - APRESENTAÇÃO RÁPIDA 3 MINUTOS

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
interface normalizada."

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
granular, e auditoria completa de cada operação."

**Tempo: 12 segundos**

---

# SLIDE 6: PADRÕES DE COMUNICAÇÃO [10 segundos]

"Três padrões de implementação: Evento para comunicação assíncrona, Orquestração
para fluxos complexos, Segurança em múltiplas camadas."

---

# SLIDE 7: RESULTADO 1 - ABSTRAÇÃO [12 segundos]

"Quatro resultados esperados:

Primeiro, abstração de APIs - cada banco em adaptador próprio, novo banco sem
impacto ao código.

Segundo, gateway robusto - transações persistidas imediatamente, retry automático,
circuit breaker. Zero perda, zero duplicação.

Terceiro, dashboard unificado - múltiplos bancos em uma tela, saldos consolidados,
relatórios exportáveis.

Quarto, inteligência preditiva - projeções de fluxo futuro, alertas de anomalias,
suporte à decisão estratégica."

---

# SLIDE 8-9-10: PRÓXIMOS PASSOS [40 segundos]

"Desenvolvimento planejado em 6 fases, 24 sprints.

Fase 1, Fundações: infraestrutura containerizada, primeiro adaptador bancário,
API Gateway funcional. Ambiente reprodutível.

Fase 2, Integração: múltiplos adaptadores de bancos reais, orquestrador
sofisticado, mecanismos de confiabilidade - retry e circuit breaker. Fluxo
end-to-end operacional."

"Fase 3, Inteligência: serviço de agregação processando eventos continuamente,
motor de projeções com modelos estatísticos, banco analítico otimizado. Primeiros
KPIs calculados.

Fase 4, Dashboard: frontend moderno e responsivo, visualizações de dados
financeiros intuitivas, interface de relatórios com exportação em múltiplos
formatos."

"Fase 5, Segurança: auditoria centralizada completa, segregação multi-tenant
rigorosa, conformidade validada com LGPD e PCI-DSS. Testes de penetração.

Fase 6, Produção: otimização de performance, escalabilidade automática,
monitoramento em tempo real, documentação operacional completa. Sistema
production-ready rodando 24/7."

---

# AGRADECIMENTO [8 segundos]

"Agradecemos ao Professor Marcelo pela orientação, à Coordenação pela infraestrutura,
e aos membros da banca pelo tempo dedicado. Muito obrigado. Ficamos à disposição
para perguntas."

---

Boa sorte! 🚀
