# Guia de Estudos – Data Warehouse, BI, OLAP e Power BI
Atualizado em: 2025-12-12

Este guia reúne as correções e os conceitos-chave cobrados nas duas provas, com resumos, mapas mentais e questões de revisão.

---

## 1) Conceitos Fundamentais

### 1.1 Data Warehouse (DW)
- Repositório orientado a análise (OLAP), histórico e integrado de múltiplas fontes.
- Cargas tipicamente em batch; também há cenários near real-time/streaming, mas não “sempre” em tempo real.
- Camadas típicas: 
  - Ingestão/Staging → Integração/Transformação → Apresentação/Consumo.
- Benefícios: qualidade e consistência, histórico, performance para análise.

### 1.2 ETL x ELT
- ETL: Extrair → Transformar → Carregar (transforma fora do DW).
- ELT: Extrair → Carregar → Transformar (usa o motor do DW/lakehouse).
- Em provas, “Transferência” não é o T do ETL.

### 1.3 Modelagem de Dados
- Relacional (OLTP): tabelas normalizadas, transações, operações do dia a dia.
- Dimensional (OLAP): desnormalização controlada; Tabela Fato (métricas) + Dimensões (contexto).
- Hierárquico: árvore. Rede: relações complexas em malha.

### 1.4 Esquemas Analíticos
- Estrela (Star): fato central + dimensões; simples e performático.
- Floco de Neve (Snowflake): dimensões normalizadas (mais complexas).
- Constelação (Galaxy): múltiplos fatos compartilhando dimensões (vários processos).

### 1.5 Data Mart e Data Lake
- Data Mart: subconjunto temático (Vendas, Finanças); pode ser dependente (do DW) ou independente.
- Data Lake: dados brutos (estruturados, semiestruturados, não estruturados); zonas bronze/prata/ouro; integra-se ao DW ou lakehouse.

### 1.6 BI, Data Mining e Metadados
- Business Intelligence: processos/ferramentas para suporte à decisão (dashboards, relatórios, modelos).
- Data Mining: descoberta de padrões (classificação, clusterização, regras de associação).
- Dicionário de Dados (metadados): catálogo de tabelas, campos, medidas, dimensões e regras.

---

## 2) OLAP e Cubos

### 2.1 Operações em Cubos
- Slice, Dice, Roll-up, Drill-down, Drill-through, Pivot.
- Objetivo: permitir agregações e análises complexas com alta performance.

### 2.2 Tipos de OLAP
- ROLAP: usa dados em bancos relacionais (SQL/visões); boa escala e flexibilidade.
- MOLAP: armazenamento multidimensional; consultas muito rápidas; pré-agregações.
- HOLAP: híbrido (detalhes no relacional, agregados no multidimensional).
- OLAP (termo geral): Processamento Analítico Online.

### 2.3 Implementação e Performance
- Criação de cubos: definição de fatos, dimensões, hierarquias, medidas e agregações.
- ETL/ELT: integrar, limpar e padronizar dados antes de popular o DW/cubos.
- Indexação/Particionamento: acelera consultas OLAP e manutenção.
- Metadados/Dicionário: governança e entendimento dos dados.

---

## 3) Power BI

- Criação de relatórios e dashboards interativos (KPI, filtros, drill-down).
- Conectores diversos, modelagem tabular, DAX, Power Query (M).
- Modos de acesso: Import, DirectQuery, Live Connection; suporta cenários em tempo quase real (streaming, push datasets).
- Compartilhamento/Governança: workspaces, apps, RLS/OLS.

---

## 4) Visualização: Dashboard, Cockpit e Relatório

- Dashboard: visão consolidada de KPIs, atualização frequente/tempo real, foco executivo.
- Cockpit: painel gerencial para controle de indicadores e metas.
- Relatório: apresentação formal e detalhada (tabelas/listagens, auditoria).

---

## 5) Correções – Prova 1

1. V/F: “Data warehouses sempre armazenam dados em tempo real.”  
   - Correto: Falso. DW é majoritariamente histórico; pode haver near real-time, mas não é regra.

2. V/F: “ETL significa Extração, Transferência e Carregamento.”  
   - Correto: Falso. É Extração, Transformação e Carga.

3. Frase: Modelo relacional para operacionais (OLTP) e análise multidimensional para DW (OLAP).  
   - Correto.

4. Correspondência – Modelos de dados  
   - Relacional → Baseado em tabelas.  
   - Dimensional → Facilita análise por meio de dimensões.  
   - Hierárquico → Estrutura de árvore.  
   - Em Rede → Relações complexas.

5. Correspondência – Arquiteturas de DW  
   - Em Camadas → Ingestão, integração/transformação, apresentação/consumo.  
   - Data Mart → Subconjunto temático do DW.  
   - Estrela → Predominantemente desnormalizado (fato + dimensões).  
   - Constelação → Combinação de múltiplos fatos/data marts.

6. Correspondência – Conceitos  
   - Data Mining → Descoberta de padrões em grandes conjuntos.  
   - Data Lake → Dados brutos em forma original.  
   - BI → Ferramentas e técnicas de apoio à decisão.  
   - Relational Database → Modelo em tabelas.

7. Frase: “ETL é necessário para integrar dados no DW.”  
   - Pegadinha: integração pode usar ETL ou ELT; dizer “necessariamente ETL” é enganoso.

---

## 6) Correções – Prova 2

1. Múltipla escolha – Power BI  
   - Correto: Permite criação de painéis interativos.

2. Múltipla escolha – Manutenção do DW  
   - Correto: Garantir a integridade e atualização dos dados.

3. Correspondência – Visualização e análise  
   - Dashboard → Visualização em tempo real/KPIs.  
   - Cockpit → Controle de indicadores.  
   - Relatório → Apresentação formal de dados.  
   - Data Mart → Subconjunto temático (não confundir com Big Data).

4. Correspondência – Modelos de maturidade (exemplo em 4 níveis)  
   - Fase 1 → Inicial.  
   - Fase 2 → Desenvolvimento/Definido.  
   - Fase 3 → Otimização/Gerenciado.  
   - Fase 4 → Verdadeiro/Otimizado (termos variam; mantenha a ordem evolutiva).

5. Múltipla escolha – Cubos de dados  
   - Correto: Permitem agregações e análises complexas.

6. Correspondência – Tipos de OLAP  
   - MOLAP → Usa armazenamento multidimensional.  
   - ROLAP → Utiliza dados em bancos relacionais.  
   - HOLAP → Combina MOLAP + ROLAP.  
   - OLAP → Processamento Analítico Online (conceito).

7. Correspondência – Técnicas de implementação  
   - Criação de cubos → Organização multidimensional.  
   - ETL → Extrair, Transformar e Carregar.  
   - Indexação → Acelera consultas OLAP.  
   - Dicionário de dados → Repositório de metadados (não é data mining).

---

## 7) Erros Comuns em Provas
- Absolutismos: “sempre”, “apenas”, “necessariamente” (ex.: DW em tempo real; ETL obrigatório).
- Confundir Data Mart com Big Data.
- Trocar ROLAP/MOLAP/HOLAP.
- Trocar “Transformação” por “Transferência” no ETL.
- Confundir camadas de DW com camadas de aplicação (apresentação/lógica/dados).

---

## 8) Mapas Mentais Rápidos

### 8.1 Tipos de OLAP
- ROLAP → Relacional → SQL/visões → Escala.  
- MOLAP → Multidimensional → Cubos pré-agregados → Velocidade.  
- HOLAP → Híbrido → Detalhe no relacional, agregados no multidimensional.

### 8.2 Esquemas
- Estrela: Fato central + Dimensões.  
- Floco de Neve: Dimensões normalizadas.  
- Constelação: Vários fatos, dimensões compartilhadas.

### 8.3 Visualizações
- Dashboard: KPI + tempo real.  
- Cockpit: Controle gerencial.  
- Relatório: Detalhe formal.

---

## 9) Questões de Revisão (pratique)
1. Cite três diferenças entre OLTP e OLAP.  
2. Dê exemplos de medidas de uma Tabela Fato e de atributos em duas Dimensões.  
3. Quando escolher ROLAP em vez de MOLAP? Justifique.  
4. Explique ETL vs ELT e dê um cenário para cada.  
5. Desenhe um esquema estrela simples para “Vendas”.  
6. Liste operações OLAP e um exemplo prático de drill-down.  
7. O que documentar em um dicionário de dados de BI?

---

## 10) Referências rápidas
- Kimball Group – Dimensional Modeling Techniques.  
- Microsoft Learn – Power BI e DAX (coleções oficiais).  
- Artigos sobre OLAP (ROLAP, MOLAP, HOLAP) e operações de cubos.

---

Boa prova e bons estudos!
