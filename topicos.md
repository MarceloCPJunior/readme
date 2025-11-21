# Guia Rápido de Estudo - Data Warehouses, OLAP e Visualização

## RESUMO EXECUTIVO - UNIDADE 3 & 4

---

## UNIDADE 3: DATA WAREHOUSES E OLAP

### 📌 AULA 01: CRIAÇÃO DE DATA WAREHOUSES

**Conceito Central:**
DW é um repositório centralizado que consolida dados de múltiplas fontes para análise, relatórios e Business Intelligence.

**Definição Rápida:**
- DW operacional: Dados operacionais, atualizações contínuas
- DW analítico: Dados históricos, atualizações periódicas

**Componentes Principais:**
1. Fontes (ERP, CRM, APIs, arquivos)
2. ETL (Extração, Transformação, Carga)
3. Staging Area (Preparação intermediária)
4. Armazenamento Central (Fatos + Dimensões)
5. Ferramentas BI (OLAP, Dashboards, Power BI)

**Arquitetura 3 Camadas (Padrão):**
```
Origem → Staging → DW Central → BI Tools
```

**Tabela de Fatos vs Dimensão:**

| Fatos | Dimensões |
|-------|-----------|
| Dados quantitativos (vendas) | Dados descritivos (quem, o quê) |
| Chaves estrangeiras | Descrevem contexto |
| Muitas linhas | Poucas linhas |
| Exemplo: Venda de 500 reais | Exemplo: Cliente João, Produto A |

**Esquemas Comuns:**

**Star Schema:**
- Tabela fatos central
- Dimensões ao redor
- Simples, rápido, menos normalizado

**Snowflake Schema:**
- Dimensões normalizadas
- Mais complexo
- Economiza espaço
- Consultas mais complexas

**Criação (Fases):**
1. Planejamento (objetivos, requisitos)
2. Design Lógico (DER, fatos/dimensões)
3. Design Físico (tabelas, storage)
4. Implementação (criar estrutura)
5. Carregamento (dados históricos)
6. Validação (qualidade, performance)

---

### 📌 AULA 02: MANUTENÇÃO DE DATA WAREHOUSES

**Tipos de Manutenção:**

**1. Manutenção de Dados**
- Atualização/Refresh: Novos dados, modificações
- Limpeza: Remove duplicatas, inconsistências
- Archiving: Dados antigos

**2. Manutenção de Performance**
- Monitoramento: CPU, memória, disk, queries
- Otimização: Índices, reorganização, estatísticas

**3. Manutenção Preventiva**
- Backup regular
- Testes de restauração
- Monitoramento de saúde
- Alertas automáticos

**4. Manutenção Corretiva**
- Resolver problemas
- Recuperar de falhas
- Data quality issues

**Processo ETL (Essencial para Manutenção):**

```
EXTRAÇÃO
├─ Completa: Todos os dados
└─ Incremental: Apenas novos/modificados
    ├─ Timestamps
    ├─ CDC (Change Data Capture)
    └─ Delta queries

TRANSFORMAÇÃO
├─ Limpeza de dados
├─ Validação
├─ Cálculos
├─ Conversões
└─ Enriquecimento

CARREGAMENTO
├─ Completo: Tudo
└─ Incremental
    ├─ Lotes
    └─ Streaming (tempo real)
```

**Ciclo de Manutenção:**
```
Operação Normal → Detecção → Diagnóstico → Resolução → Verificação → Otimização → Volta
```

**Ferramentas ETL Populares:**
- SQL Server Integration Services (SSIS)
- Apache Airflow
- Talend
- Informatica
- Databricks

**Métricas Importantes:**
- SLA: Uptime (99.9%), RTO, RPO
- KPIs: Taxa de erro, performance, fragmentação

---

### 📌 AULA 03: OLAP (Online Analytical Processing)

**Definição:**
OLAP permite análise rápida de dados multidimensionais em múltiplas perspectivas.

**OLAP vs OLTP:**

| OLAP (Análise) | OLTP (Operação) |
|---|---|
| Dados históricos | Dados atuais |
| Multidimensional | Normalizado |
| Complexas, analíticas | Simples, transacionais |
| Segundos/minutos | Milissegundos |
| Analistas | Usuários finais |

**Cubo OLAP:**
Estrutura multidimensional com Dimensões (categorias) e Medidas (números).

Exemplo:
- Dimensões: Tempo (Ano, Mês, Dia), Local (País, Estado, Cidade), Produto, Cliente
- Medidas: Vendas, Custo, Lucro, Quantidade

**Hierarquias em Dimensões:**
```
Tempo:
├─ Ano
│  ├─ Trimestre
│  │  ├─ Mês
│  │  │  └─ Dia

Localização:
├─ País
│  └─ Estado
│     └─ Cidade
```

---

### 📌 AULA 04: TÉCNICAS DE IMPLEMENTAÇÃO OLAP

**Operações Principais em OLAP:**

**1. Drill-Down (Aprofundar)**
```
Vendas Brasil 2024 (Total)
        ↓
Vendas São Paulo, Minas Gerais, RJ (Estados)
        ↓
Vendas São Paulo, Campinas, Santos (Cidades)
```
Desce em hierarquia, aumenta detalhe

**2. Roll-Up (Agregar)**
```
Vendas por Dia
    ↑
Vendas por Semana
    ↑
Vendas por Mês
    ↑
Vendas por Ano
```
Sobe em hierarquia, reduz detalhe (inverso de drill-down)

**3. Slice (Corte)**
Fixa uma dimensão em valor específico:
- "Mostrar vendas de 2024" (sem especificar região/produto)
- Reduz um cubo multidimensional

**4. Dice (Múltiplos Cortes)**
Seleciona múltiplas dimensões:
- "Vendas de 2024, SP e MG, produtos A e B"

**5. Pivot (Rotação)**
Reposiciona dimensões para nova perspectiva:
```
Antes: Linhas = Região, Colunas = Trimestre
Depois: Linhas = Trimestre, Colunas = Região
```

---

### 📌 AULA 05: MOLAP, ROLAP, HOLAP (Professor)

**Três Tipos de OLAP:**

**MOLAP (Multidimensional OLAP)**
- Armazenamento: Estrutura multidimensional (hipercubo)
- Agregações: Pré-calculadas
- Performance de Consulta: ⭐⭐⭐⭐⭐ Excelente
- Performance de Carga: ⭐ Lenta
- Espaço: Alto
- Quando usar: Dados que não mudam frequentemente, queries complexas
- Exemplo: Análise de vendas mensais

**ROLAP (Relational OLAP)**
- Armazenamento: Tabelas relacionais (Star/Snowflake)
- Agregações: On-the-fly (sob demanda)
- Performance de Consulta: ⭐⭐⭐ Boa
- Performance de Carga: ⭐⭐⭐⭐⭐ Rápida
- Espaço: Baixo
- Quando usar: Dados em tempo real, muito volume, flexibilidade
- Exemplo: Logs de web servers (bilhões de eventos)

**HOLAP (Hybrid OLAP)**
- Armazenamento: Híbrido (MOLAP + ROLAP)
- Agregações: Pré-calculadas + on-the-fly
- Performance de Consulta: ⭐⭐⭐⭐ Muito Boa
- Performance de Carga: ⭐⭐⭐ Média
- Espaço: Médio
- Quando usar: Equilíbrio entre performance e flexibilidade
- Exemplo: Análise de vendas com atualizações frequentes

**Comparação Rápida:**

| Critério | MOLAP | ROLAP | HOLAP |
|----------|-------|-------|-------|
| Velocidade Consulta | ⭐⭐⭐⭐⭐ | ⭐⭐⭐ | ⭐⭐⭐⭐ |
| Velocidade Carga | ⭐ | ⭐⭐⭐⭐⭐ | ⭐⭐⭐ |
| Espaço Disco | Alto | Baixo | Médio |
| Atualização | Periódica | Contínua | Frequente |

**Processo OLAP:**
```
1. Definir Requisitos (dimensões, medidas, hierarquias)
2. Design Lógico (estrutura cubo)
3. Design Físico (tipo OLAP, storage)
4. Implementação (ferramenta)
5. Processamento (carregar, calcular)
6. Validação (queries, performance)
7. Implantação (produção)
```

**Ferramentas OLAP:**
- Microsoft SQL Server Analysis Services (SSAS)
- Mondrian (open source, ROLAP)
- Oracle OLAP
- IBM Cognos

---

### 📌 AULA 06: ESTUDO DE CASO - MOEDAS DIGITAIS

**Blockchain/Bitcoin Analysis com OLAP:**

**Desafios:**
- Volume massivo (600k Bitcoin transactions/dia, 1.5M Ethereum/dia)
- Crescimento contínuo
- Análises complexas (rastreamento de fundos)

**Recomendação:** HOLAP ou ROLAP (não MOLAP)
- Razão: Muito volume, dados crescem forever

**Dimensões Ideais:**
- Tempo (Ano, Mês, Dia, Hora, Minuto)
- Ator (Remetente, Destinatário)
- Tipo de Transação
- Faixa de Valor

**Medidas:**
- Quantidade de transações
- Valor total
- Taxa média
- Tempo de confirmação

**Análises Possíveis:**
- Whale watching (grandes transferências)
- Detecção de fraude
- Análise de padrão
- Rastreamento de fundos

---

## UNIDADE 4: VISUALIZAÇÃO DE DADOS E BI

### 📌 AULA 01: OPERAÇÕES SOBRE CUBOS

As 5 operações fundamentais já explicadas acima (Drill-Down, Roll-Up, Slice, Dice, Pivot).

**Exemplo Integrado:**
```
Cubo Original: Vendas[Produto, Região, Período, Categoria]

1. Slice por período 2024
   → Vendas[Produto, Região, Categoria] apenas 2024

2. Drill-Down em Região
   → De Regiões para Estados

3. Pivot
   → Linhas = Produto, Colunas = Período

4. Dice adicional
   → Apenas produtos A, B, C; periodos Q1, Q2
```

---

### 📌 AULA 02: MODELO DE MATURIDADE DO DATA WAREHOUSE

**Níveis de Maturidade:**

**Nível 1: Inicial (Ad Hoc)**
- Sem DW formal
- Relatórios manuais (Excel)
- Dados em múltiplas fontes
- Inconsistência
- Tempo: ~6 meses para evolução

**Nível 2: Repetível (Departamental)**
- Data Marts departamentais
- ETL definido
- Qualidade melhorada
- Tempo: 1-2 anos

**Nível 3: Definido (Corporativo)** ← Alvo típico
- DW corporativo
- ETL padronizado
- Governança de dados
- Tempo: 2-3 anos

**Nível 4: Gerenciado (Otimizado)**
- DW otimizado
- SLAs definidos
- Monitoramento contínuo
- Tempo: 1-2 anos

**Nível 5: Otimizado (Inteligente)**
- IA e ML integrados
- Previsões automáticas
- Real-time analytics
- Tempo: 1-2 anos

**Evolução Típica:**
```
Inicial → Repetível → Definido → Gerenciado → Otimizado
(6m)    (1-2a)      (2-3a)      (1-2a)       (1-2a)
```

---

### 📌 AULA 03: VISUALIZAÇÃO E ANÁLISE DE DADOS

**Tipos de Gráficos e Quando Usar:**

| Gráfico | Uso | Exemplo |
|---------|-----|---------|
| Barra/Coluna | Comparar categorias | Vendas por região |
| Linha | Tendência no tempo | Vendas mensais |
| Pizza | Proporções de um todo | % de mercado por segmento |
| Dispersão | Correlação 2 variáveis | Preço vs Quantidade |
| Área | Evolução acumulada | Receita crescente |
| Mapa | Dados geográficos | Vendas por estado |

**Princípios de Bom Design:**

✅ **Clareza**
- Título claro
- Eixos bem rotulados
- Legenda visível
- Sem elementos desnecessários

✅ **Acurácia**
- Dados corretos
- Escala apropriada
- Sem distorções

✅ **Eficiência**
- Transmitir insight rapidamente
- Não sobrecarregar
- Destacar importante

✅ **Estética**
- Cores harmônicas
- Fonte legível
- Espaçamento adequado

**Acessibilidade:**
- Considerar daltonismo (8% homens)
- Evitar vermelho + verde juntos
- Usar múltiplas codificações (cor + padrão)

---

### 📌 AULA 04: DASHBOARD E COCKPIT

**Dashboard Executivo:**
- Alto nível, KPIs
- 5-10 visualizações
- Atualização diária/semanal
- Para decisões estratégicas
- Exemplo: Dashboard de vendas

**Cockpit Operacional:**
- Detalhes, operações
- 15-20+ visualizações
- Atualização real-time
- Para monitoramento contínuo
- Alertas automáticos
- Exemplo: Cockpit de produção

**Diferenças Principais:**

| Aspecto | Dashboard | Cockpit |
|--------|-----------|---------|
| Público | Executivos | Operadores |
| Nível | Alto | Detalhes |
| Atualização | Periódica | Real-time |
| Ação | Decisões | Operações |
| Foco | Tendências | Desvios |

---

### 📌 AULA 05: POWER BI

**O que é:**
Plataforma Microsoft de Business Intelligence que transforma dados em visualizações interativas.

**Componentes:**
- **Power BI Desktop:** Aplicativo para criar (GRATUITO)
- **Power BI Service:** Cloud para publicar (R$ 50/mês)
- **Power BI Mobile:** App para celular

**Fluxo de Trabalho:**
```
Conectar Dados → Transformar (Power Query) → Modelar → Visualizar → Publicar
```

**Funcionalidades:**
- ✅ 200+ conectores de dados
- ✅ 45+ tipos de visualizações
- ✅ Integração Microsoft (Excel, Teams)
- ✅ DAX para cálculos complexos
- ✅ Segurança enterprise
- ✅ Compartilhamento fácil

**Power Query (Transformação):**
- Interface visual low-code
- Limpeza e validação
- Combinação de fontes
- Colunas calculadas

**Modelagem:**
- Relacionamentos
- Hierarquias
- DAX (linguagem de cálculo)
- Medidas e métricas

**DAX (Data Analysis Expressions) - Exemplos:**
```
Total = SUM(Vendas[Valor])

Acima Meta = CALCULATE(SUM(Vendas), Vendas > Meta)

YTD = CALCULATE(SUM(Vendas), DATESYTD(Data[Data]))
```

**Preços:**
- Desktop: GRATUITO
- Power BI Pro: ~R$ 50/mês/usuário
- Power BI Premium: ~R$ 500-5000/mês (sem limite usuários)

**Vantagens:**
- Fácil uso
- Integração Microsoft
- Comunidade grande
- Bom custo-benefício
- Atualizações frequentes

---

## QUESTÕES PROVÁVEIS DE PROVA (COM RESPOSTAS)

### Nível Fácil

**P: O que é um Data Warehouse?**
R: Repositório centralizado que consolida dados de múltiplas fontes, organizados para análise e Business Intelligence.

**P: Qual é a diferença entre tabela de fatos e dimensão?**
R: Fatos armazenam medidas numéricas (vendas, custos). Dimensões armazenam atributos descritivos (cliente, produto, data).

**P: O que é OLAP?**
R: Processamento Analítico Online, permite análise rápida de dados multidimensionais em múltiplas perspectivas.

---

### Nível Médio

**P: Explique as diferenças entre MOLAP, ROLAP e HOLAP.**
R: MOLAP pré-calcula em estrutura multidimensional (rápido, longo processamento). ROLAP calcula sob demanda em tabelas relacionais (processamento rápido, consultas mais lentas). HOLAP combina ambos (equilíbrio).

**P: O que é drill-down em um cubo OLAP?**
R: Aumentar nível de detalhe descendo em hierarquia dimensional (ex: Ano → Trimestre → Mês → Dia).

**P: Como escolher entre Star Schema e Snowflake?**
R: Star Schema é simpler, rápido, menos normalizado. Snowflake é mais normalizado, economiza espaço, mas consultas mais complexas.

**P: Qual é a diferença entre Dashboard e Cockpit?**
R: Dashboard é para visão estratégica (alto nível, decisões executivas). Cockpit é para monitoramento operacional (tempo real, alertas).

---

### Nível Difícil

**P: Descreva o processo completo de implementação de um Data Warehouse.**
R: 1) Planejamento e requisitos, 2) Design lógico (DER), 3) Design físico (tabelas), 4) Implementação (criar estrutura), 5) Carregamento (ETL), 6) Validação (testes), 7) Implantação (produção) e manutenção contínua.

**P: Por que um cubo OLAP seria melhor que queries SQL diretas para análise?**
R: OLAP oferece navegação multidimensional intuitiva (drill-down, pivot), agregações pré-calculadas (rápido), visualizações interativas, e insigts ágeis sem escrever SQL complexo.

**P: Em um projeto de análise de 10 bilhões de transações de blockchain, qual tipo OLAP você escolheria e por quê?**
R: ROLAP ou HOLAP. Razão: Volume massivo (MOLAP seria impraticável), dados crescem continuamente (MOLAP reprocessaria tudo), precisa flexibilidade. ROLAP aceita atualização incremental e escala bem.

**P: Como o Power BI se integra com todo o ecossistema de BI?**
R: Power BI conecta múltiplas fontes (SQL, Excel, APIs), transforma dados (Power Query), cria modelo semântico, visualiza (45+ gráficos), compartilha em cloud (Service), integra com Teams/Office, e oferece mobile access.

---

## CHECKLIST PRÉ-PROVA

- [ ] Entendi diferença entre DW e banco transacional
- [ ] Sei componentes de uma arquitetura DW
- [ ] Conheço Star Schema vs Snowflake
- [ ] Entendo ETL (Extração, Transformação, Carga)
- [ ] Sei o que é OLAP e para que serve
- [ ] Conheço MOLAP, ROLAP, HOLAP com diferenças
- [ ] Entendo operações: Drill-down, Roll-up, Slice, Dice, Pivot
- [ ] Conheço tipos de gráficos e seus usos
- [ ] Diferencio Dashboard de Cockpit
- [ ] Conheço Power BI (componentes, DAX, preços)
- [ ] Entendo Modelo de Maturidade (5 níveis)
- [ ] Sei princípios de bom design visual

---

## DICAS DE ESTUDO

✅ **Entenda os conceitos antes de memorizar**
✅ **Use exemplos práticos**
✅ **Compare MOLAP vs ROLAP vs HOLAP**
✅ **Visualize arquiteturas (desenhe diagramas)**
✅ **Pratique identificar melhor tipo de gráfico**
✅ **Estude casos de uso reais**
✅ **Revise os 5 níveis de maturidade**

---

Boa sorte na prova! 🎓
