# Guia de Estudo Rápido para Prova - Criptografia Assimétrica e Certificação Digital

## RESUMO EXECUTIVO POR AULA

---

## UNIDADE 3 - ALGORITMOS CRIPTOGRÁFICOS ASSIMÉTRICOS

### ⭐ AULA 01: CSPRNG

**Conceito Central:**
Um gerador que produz números verdadeiramente aleatórios para uso em criptografia, impossíveis de prever mesmo sabendo os valores anteriores.

**Características Essenciais:**
- ✅ Resistente à previsão
- ✅ Irreversível
- ✅ Passa em testes estatísticos rigorosos
- ✅ Alta entropia

**Diferença Crítica (PRNG vs CSPRNG):**
- PRNG: Simula aleatoriedade (simulações, jogos)
- CSPRNG: Verdadeiramente aleatório (chaves, segurança)

**Aplicações Vitais:**
- Geração de chaves criptográficas
- Geração de nonces
- Assinaturas digitais

**Algoritmos Principais:**
1. HMAC-DRBG: Estado duplo (K, V), muito seguro
2. SHA-256 DRBG: Mais simples, segurança boa

---

### ⭐ AULA 02: CRIPTOGRAFIA DE CHAVE PÚBLICA

**Princípio Revolucionário (1976):**
Duas chaves diferentes: pública (divulga) e privada (guarda)

**Fluxo Básico:**
```
Remetente → chave pública do destinatário → criptografa
Criptografia enviada →
Destinatário → chave privada (só ele tem) → descriptografa
```

**Garantias Fornecidas:**
- Confidencialidade: Só quem tem chave privada acessa
- Autenticação: Criptografar com privada prova identidade
- Não-repúdio: Não pode negar o que assinou

**Vantagem Suprema:**
Elimina problema de troca segura de chaves (problema crítico da simétrica)

**Padrão Atual (Híbrido):**
- Assimétrica: Distribuir chave de sessão (segura)
- Simétrica: Criptografar dados (eficiente)

---

### ⭐ AULA 03: RSA

**O Algoritmo do Mundo:**
90% das implementações de criptografia pública usam RSA

**Base Matemática:**
Fatorar dois primos grandes é computacionalmente impossível

**Processo de Geração de Chaves:**

```
1. Escolher dois primos grandes: p e q
2. Calcular n = p × q
3. Calcular φ(n) = (p-1) × (q-1)
4. Escolher e (expoente público): 1 < e < φ(n) e mdc(e,φ(n))=1
   → Comumente: e = 65.537
5. Calcular d (expoente privado): (e × d) mod φ(n) = 1
   → d é inverso multiplicativo de e

Resultado:
- Chave Pública: (e, n)
- Chave Privada: (d, n)
```

**Operações:**

Criptografia: C = M^e mod n (elevado a e)
Descriptografia: M = C^d mod n (elevado a d)

**Tamanhos Recomendados:**
- 512 bits: ❌ Quebrado
- 1024 bits: ❌ Inseguro
- 2048 bits: ✅ Seguro até 2030
- 4096 bits: ✅ Seguro longo prazo

**Segurança em Números:**
Fatorar 2048 bits = bilhões de anos com computadores atuais

**Ameaça Futura:**
Computadores quânticos podem quebrar RSA em tempo polinomial

---

### ⭐ AULA 04: PGP (Pretty Good Privacy)

**Filosofia:**
Privacidade é direito, não privilégio. Descentralizado, sem autoridades centrais.

**Tipo de Sistema:**
HÍBRIDO: Combina simetria (rápido) + assimetria (seguro)

**Fluxo de Encriptação PGP:**

```
Mensagem Original
    ↓
1. COMPRESSÃO
   └─ Reduz tamanho, aumenta segurança
    ↓
2. CHAVE DE SESSÃO ALEATÓRIA
   └─ Gerada por mouse/teclado + teste de primalidade
    ↓
3. CRIPTOGRAFIA SIMÉTRICA (IDEA/AES-256)
   └─ Criptografa dados
    ↓
4. RSA CRIPTOGRAFIA (Assimétrica)
   └─ Criptografa chave de sessão com chave pública do destinatário
    ↓
SAÍDA: Dados criptografados + Chave de sessão encriptada
```

**Assinatura Digital no PGP:**
```
Mensagem
    ↓
Hash (SHA-1/SHA-256)
    ↓
Encripta com chave PRIVADA
    ↓
ASSINATURA DIGITAL
    ↓
Verificação:
- Descriptografa com chave PÚBLICA
- Recalcula hash
- Compara = AUTÊNTICO
```

**Modelo de Confiança: Web of Trust**
- Descentralizado (vs autoridades certificadoras)
- Cada usuário atesta identidade de outros
- Formação emergente de confiança
- Flexível, menos formal

**Vantagens do PGP:**
- Criptografia provada matematicamente
- Descentralizado (sem ponto único de falha)
- Auditado pela comunidade
- Código aberto

---

### ⭐ AULA 05: TÓPICOS AVANÇADOS

**Variações de RSA:**
- OAEP: Adiciona padding aleatório (mais seguro)
- RSASSA-PSS: Assinatura probabilística (mais segura)

**Alternativas ao RSA (Futuro):**
- **ECC (Curvas Elípticas):** 256-bit ECC ≈ 3072-bit RSA
- **ECDSA:** Assinatura em curvas elípticas (Bitcoin usa)
- **Diffie-Hellman:** Acordo de chave (não encriptação)

**Ameaça: Computadores Quânticos**
- Algoritmo Shor quebra RSA, ECC, DH em tempo polinomial
- Pesquisa: Post-Quantum Cryptography
- Alternativas: Lattice-based, Hash-based

**Segurança Longo Prazo:**
- Perfect Forward Secrecy: Histórico seguro mesmo se chave comprometida
- Key Rotation: Trocar chaves periodicamente
- Monitoring: Detecção de anomalias

---

### ⭐ AULA 06: MOEDAS DIGITAIS (BLOCKCHAIN)

**Bitcoin = Criptografia Assimétrica em Ação**

**Componentes Criptográficos:**
1. **SHA-256 (Hashing):** Identifica blocos, prova de trabalho
2. **ECDSA (Assinatura):** Autoriza transações, não-repúdio
3. **Chave Pública/Privada:** Propriedade de moedas

**Processo de Transação:**
```
Alice prepara envio
    ↓
Assina com chave PRIVADA (ECDSA)
    ↓
Rede verifica com chave PÚBLICA de Alice
    ↓
Transação entra no pool
    ↓
Mineradores calculam Proof of Work
    ↓
Bloco adicionado à cadeia
    ↓
Transação IRREVERSÍVEL (após ~6 confirmações)
```

**Blockchain: Corrente de Blocos**
```
[Bloco 1] → [Bloco 2] → [Bloco 3]
  Hash0      Hash1      Hash2
  Dados      Dados      Dados
```
- Cada bloco aponta para anterior
- Alterar um bloco invalida tudo posterior
- Descentralizado: cópias em milhares de nós

**Criptomoeda vs Moeda Digital:**

| Aspecto | Criptomoeda | Moeda Digital |
|---------|-----------|--------------|
| Controle | Descentralizado | Centralizado |
| Tecnologia | Blockchain | Centralizada |
| Segurança | Muito alta | Boa |
| Reversibilidade | Quase impossível | Possível |

**Exemplo: Bitcoin (e Ethereum, Litecoin, etc.)**
- Descentralizado: Sem banco central
- Pseudoanônimo: Público, mas sob endereços
- Seguro: Criptografia + descentralização
- Lento: ~7 tx/seg (Bitcoin), ~15 tx/seg (Litecoin)

---

## UNIDADE 4 - CERTIFICAÇÃO DIGITAL

### ⭐ AULA 01: PRINCÍPIOS

**Definição:**
Usar criptografia para verificar identidade e garantir autenticidade em transações digitais

**Pilares da Segurança:**

1. **Autenticação:** Identidade verificada e impossível falsificar
2. **Integridade:** Documentos não podem ser alterados
3. **Confidencialidade:** Acesso restrito aos autorizados
4. **Não-repúdio:** Impossível negar ação assinada

**Assinatura Digital ≠ Eletrônica:**

| Aspecto | Digital | Eletrônica |
|---------|---------|-----------|
| Tecnologia | Criptografia PKI | Qualquer método |
| Segurança | Muito Alta | Variável |
| Lei | Plena (específica) | Plena (casos) |
| Repúdio | Impossível | Possível |

---

### ⭐ AULA 02: CERTIFICADO DIGITAL

**O que é:**
Documento eletrônico que une:
- Chave pública de usuário
- Dados de identificação
- Assinatura digital da AC

É um "RG Digital" confiável

**Padrão: X.509v3 (Internacional)**

Contém:
- Versão
- Número de série (único)
- Período de validade
- Dados do titular
- Chave pública (2048 bits RSA)
- Extensões (uso autorizado)
- Assinatura da AC (valida tudo)

**Tipos Brasileiros:**

| Tipo | Validade | Armazenamento | Segurança | Uso |
|------|----------|---------------|-----------|-----|
| **A1** | 1 ano | Arquivo | Baixa | Básico |
| **A3** | 5 anos | Token USB | Alta | Importante |

**Tipos por Titular:**
- e-CPF: Pessoa física
- e-CNPJ: Pessoa jurídica

---

### ⭐ AULA 03: AUTORIDADES CERTIFICADORAS

**Função:**
Empresa pública/privada que emite certificados após verificar identidade

**É como um Cartório, mas digital**

**Hierarquia:**

```
AC-Raiz (topo, máxima confiança)
    ↓
ACs Intermediárias
    ↓
ACs de Segundo Nível
    ↓
Usuários com Certificados
```

**Responsabilidades da AC:**
- ✅ Verificar identidade presencialmente
- ✅ Gerar pares de chaves
- ✅ Emitir certificados
- ✅ Manter lista de revogação
- ✅ Revogar se necessário
- ✅ Proteger chave privada própria

**Confiança em uma AC:**
- Credenciamento em AC superior
- Conformidade com normas
- Transparência (publicar procedimentos)
- Auditoria independente
- Responsabilidade legal

---

### ⭐ AULA 04: ICP-BRASIL

**Nome Oficial:**
Infraestrutura de Chaves Públicas Brasileira

**Objetivo:**
Sistema hierárquico nacional para certificação digital segura e legal

**Criação:**
- 2001: Medida Provisória 2.200-2
- 2006: Lei 11.419 (processo eletrônico)

**Topo: AC-Raiz (ITI)**
- Instituto Nacional de Tecnologia da Informação
- Define políticas e normas
- Emite certificados de ACs intermediárias
- Chave privada em sala-cofre ultrassegura
- Responsável por auditoria

**Hierarquia Brasileira:**
```
┌─────────────────────┐
│  AC-Raiz (ITI)      │
└──────────┬──────────┘
           │
    ┌──────┴──────┐
    ↓             ↓
[AC Nível 1]  [AC Nível 1]
    │             │
  ┌─┴─┐         ┌─┴─┐
  ↓   ↓         ↓   ↓
[AC2º][AC2º]  [AC2º][AC2º]
  │   │         │   │
  ↓   ↓         ↓   ↓
[USUÁRIOS COM CERTIFICADOS]
```

**Comitê Gestor:**
- Órgão supervisor
- Define políticas
- Governo + iniciativa privada + sociedade civil

**ACs Credenciadas Exemplos:**
- Serpro
- Serasa Experian
- Soluti
- ACT BRY
- Imprensa Oficial

**Aplicações:**
- Processos administrativos eletrônicos
- Assinatura de contratos
- NFe (Nota Fiscal Eletrônica)
- Operações bancárias
- Medicina digital

---

### ⭐ AULA 05: TÓPICOS EM CERTIFICAÇÃO

**Revogação de Certificados**

Motivos:
- Chave privada comprometida
- Usuário deixa organização
- Dados desatualizados
- Erro de emissão

Métodos:
- **CRL (Certificate Revocation List):** Lista periódica
- **OCSP (Online Certificate Status Protocol):** Consulta em tempo real

**Validação de Certificados**

Processo:
```
1. Verifica assinatura da AC
2. Valida período de vigência
3. Verifica cadeia até AC-Raiz
4. Consulta status (CRL/OCSP)
5. Valida contra políticas locais
```

**Extensões (Funcionalidades Adicionais)**

- Key Usage: Digital Signature, Non-Repudiation
- Extended Key Usage: Web Server Auth, Email, Time Stamping
- Subject Alternative Name: Domínios alternativos
- Authority Key Identifier: Chave da AC que emitiu

**Timestamp (Hora Certificada)**
- Prova que documento existia em determinada data/hora
- Não-repúdio temporal
- Validade jurídica permanente

---

### ⭐ AULA 06: SSL/TLS, OPENSSL, HEARTBLEED

**SSL/TLS: Protocolos de Segurança Web**

Função: Garantir comunicação segura entre navegador e servidor HTTPS

Evolução:
- SSL 3.0 ❌ Obsoleto
- TLS 1.0 ❌ Legado
- TLS 1.2 ✅ Atual
- TLS 1.3 ✅ Moderno

**Handshake TLS (Aperto de Mão):**
```
1. Client Hello: Versão, ciphers suportados, número aleatório
2. Server Hello: Versão, cipher escolhido, número aleatório
3. Server Certificate: Certificado do servidor (chave pública)
4. Server Key Exchange: Parâmetros, assinado
5. Client Key Exchange: Pré-chave mestre criptografada
6. Ambos trocam chave de sessão simétrica
7. FINISHED: Confirma sucesso
```

Resultado: Chave de sessão simétrica compartilhada, todos dados criptografados

**OpenSSL: Implementação Padrão**

Biblioteca de código aberto de SSL/TLS
- Gera chaves RSA
- Cria certificados
- Estabelece conexões TLS
- Padrão da indústria
- Usado em 99% dos servidores

Versões:
- 1.0.2: LTS (fim de suporte 2019)
- 1.1.1: LTS (atual recomendado)
- 3.0: Novo

**HEARTBLEED (CVE-2014-0160) - A VULNERABILIDADE**

Data: 7 de abril de 2014
Severidade: **CRÍTICA** (9.8/10)
Afetou: ~2 milhões de websites (17% internet)

**O que é Heartbeat:**
Extensão TLS que verifica se conexão está viva
- Cliente: "Olá, você está aí?"
- Servidor: "Sim, estou aqui"

**O BUG:**

```
NORMAL:
Cliente envia: "Olá" [Tamanho: 4 bytes]
Servidor responde: "Olá"

HEARTBLEED:
Cliente envia: "Olá" [Tamanho: 64.000 bytes] ← MENTIRA!
Servidor responde: "Olá" + [próximos 63.996 bytes da MEMÓRIA]
                     ↓
            Atacante consegue: CHAVES PRIVADAS! Senhas! Dados!
```

**Problema Técnico:**
OpenSSL não validava corretamente tamanho do payload
Retornava quantidade de bytes solicitada sem verificar se havia dados

**Dados Vazados:**
- ⚠️ Chaves privadas do servidor (CRÍTICO!)
- Senhas de usuários
- Nomes de usuários
- Tokens de sessão
- Qualquer coisa na memória

**Versões Afetadas:**
OpenSSL 1.0.1 até 1.0.1f (inclusive)

**Websites Impactados:**
Yahoo, GitHub, Tumblr, OkCupid, Dropbox, Amazon, milhares outros

**Resposta (Patch):**

```
1. Atualizar para OpenSSL 1.0.1g (lançado 7/4/2014)
2. Validação corrigida de tamanho de payload
3. Limite de tamanho máximo implementado
4. Verificação de limites
5. Revogação de certificados comprometidos
6. Emissão de novos certificados
7. Força troca de senhas
```

**Lições Aprendidas:**

✅ Auditoria de código essencial
✅ Fuzzing detectaria bug
✅ Divulgação responsável foi implementada
✅ Necessidade de atualização rápida
✅ Monitoramento contínuo obrigatório

**Segurança Moderna:**
- OpenSSL atualizado
- TLS 1.3 (redesenho completo)
- Perfect Forward Secrecy
- Certificate Pinning
- HSTS (força HTTPS)

---

## DICAS FINAIS PARA PROVA

### Memorização de Fórmulas/Conceitos

**RSA:**
```
n = p × q
φ(n) = (p-1) × (q-1)
(e × d) mod φ(n) = 1
C = M^e mod n
M = C^d mod n
```

**Validação de Certificado:**
1. Assinatura da AC
2. Período de vigência
3. Cadeia até raiz
4. Status de revogação
5. Políticas locais

**Hierarquia ICP-Brasil:**
AC-Raiz (ITI) → ACs Nível 1 → ACs Nível 2 → Usuários

### Palavras-Chave para Responder

| Conceito | Palavras-Chave |
|----------|---|
| CSPRNG | Aleatório, imprevisível, irreversível, chaves, entropia |
| RSA | Primos, fatoração, 2048 bits, chave pública/privada |
| PGP | Híbrido, simétrica+assimétrica, web of trust |
| Blockchain | Hash, ECDSA, descentralizado, imutável, irreversível |
| Certificado | X.509, AC, chave pública, integridade, autenticação |
| ICP-Brasil | Hierárquica, ITI, AC-Raiz, legal, Brasil |
| Heartbleed | Memória, vazamento, chaves privadas, OpenSSL 1.0.1 |

### Comparações Rápidas

**Simétrica vs Assimétrica:**
- Simétrica: Uma chave, rápida, problema de troca
- Assimétrica: Duas chaves, lenta, sem problema de troca

**A1 vs A3:**
- A1: 1 ano, arquivo, portável, menos seguro
- A3: 5 anos, token, seguro, precisa leitor

**Blockchain vs Banco:**
- Blockchain: Descentralizado, imutável, lento
- Banco: Centralizado, reversível, rápido

**TLS 1.2 vs TLS 1.3:**
- 1.2: Atual, seguro
- 1.3: Mais rápido, mais seguro, zero-RTT

---

## QUESTÕES PROVÁVEIS DE PROVA (COM RESPOSTAS)

### Nível Fácil

**P: O que é um CSPRNG e por que é importante?**
R: CSPRNG (Cryptographically Secure PRNG) é um gerador que produz números verdadeiramente aleatórios impossíveis de prever, essencial para gerar chaves criptográficas seguras.

**P: Qual é o tamanho de chave RSA recomendado atualmente?**
R: 2048 bits é seguro até 2030; 4096 bits para segurança longo prazo.

**P: O que significa não-repúdio?**
R: O usuário não pode negar ter realizado uma ação (assinado), pois existe prova criptográfica.

---

### Nível Médio

**P: Como funciona o processo de encriptação com PGP?**
R: (1) Mensagem comprimida, (2) Chave de sessão aleatória gerada, (3) Dados criptografados com simétrica, (4) Chave de sessão criptografada com RSA, (5) Tudo enviado junto.

**P: Qual é a hierarquia da ICP-Brasil e qual a função de cada nível?**
R: AC-Raiz (define políticas) → ACs Nível 1 (intermediárias) → ACs Nível 2 (usuários finais). Cada nível credencia e audita o inferior.

**P: Como o Heartbleed funciona?**
R: Cliente envia "Olá" mas diz que tem 64KB, servidor retorna "Olá" + dados da memória, vazando informações sensíveis da memória do servidor.

---

### Nível Difícil

**P: Explique por que RSA é considerado seguro baseado em teoria de números.**
R: RSA é seguro porque é fácil multiplicar dois primos grandes (pq=n) mas computacionalmente impossível fatorar n de volta em p e q. O algoritmo mais rápido (NFS) é exponencial, levando bilhões de anos.

**P: Compare blockchain (Bitcoin) com sistema bancário centralizado em termos de segurança criptográfica.**
R: Bitcoin usa ECDSA + SHA-256 + descentralização (milhares de cópias). Qualquer alteração invalida a cadeia. Banco centralizado usa SSL/TLS. Bitcoin é mais seguro criptograficamente mas lento; banco é rápido mas reversível.

**P: Por que Perfect Forward Secrecy é importante em TLS?**
R: PFS garante que mesmo se a chave privada do servidor for comprometida no futuro, as sessões passadas permanecessem seguras porque cada sessão usou uma chave diferente.

---

## CHECK-LIST PRÉ-PROVA

- [ ] Entendi diferença PRNG vs CSPRNG
- [ ] Sei gerar chaves RSA (passos)
- [ ] Conheço funcionamento PGP (híbrido)
- [ ] Entendi blockchain (Bitcoin)
- [ ] Sei o que é certificado X.509
- [ ] Conheço hierarquia ICP-Brasil
- [ ] Entendo Heartbleed (vazamento memória)
- [ ] Sei diferenciar A1 vs A3
- [ ] Conheço pilares de segurança (4)
- [ ] Sei validar certificado (5 passos)
- [ ] Entendo assinatura digital
- [ ] Conheço algoritmos comuns (RSA, ECDSA, SHA-256)

Boa sorte na prova! 🚀
