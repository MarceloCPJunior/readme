# Estudo Completo: Criptografia Assimétrica e Certificação Digital

## UNIDADE 3 - ALGORITMOS CRIPTOGRÁFICOS ASSIMÉTRICOS

---

### AULA 01 - GERADORES DE NÚMEROS PSEUDO-ALEATÓRIOS CRIPTOGRÁFICOS (CSPRNG)

#### O que é CSPRNG?

Um **Gerador de Números Pseudo-Aleatórios Criptograficamente Seguro (CSPRNG)** é um algoritmo especial projetado para gerar números aleatórios que são adequados para aplicações criptográficas. Diferencia-se de um PRNG comum pela sua resistência a ataques e imprevisibilidade.

#### Diferenças entre PRNG e CSPRNG

| Aspecto | PRNG | CSPRNG |
|--------|------|--------|
| **Previsibilidade** | Previsível com conhecimento da semente | Imprevisível, resistente a ataques |
| **Aplicação** | Simulações, jogos, aplicações gerais | Criptografia, geração de chaves |
| **Entropia** | Entropia limitada | Entropia de alta qualidade |
| **Reversibilidade** | Pode ser revertido | Irreversível |
| **Testes Estatísticos** | Satisfaz testes básicos | Passa em testes estatísticos rigorosos |

#### Propriedades Essenciais do CSPRNG

1. **Resistência à Previsão**: Impossível prever sequências futuras conhecendo-se valores anteriores
2. **Irreversibilidade**: Mesmo com acesso ao estado interno roubado, não é possível recuperar sequências passadas
3. **Fortuidade**: A saída deve parecer totalmente aleatória em testes estatísticos

#### Aplicações Críticas do CSPRNG

- **Geração de Chaves Criptográficas**: A segurança da chave depende da qualidade do CSPRNG
- **Geração de Nonces**: Números únicos e aleatórios para protocolos
- **Cifras de Uso Único**: Garantem sigilo perfeito
- **Sais em Esquemas de Assinatura**: ECDSA, RSASSA-PSS
- **Gerenciamento de Cookies e Tokens**: Segurança em aplicações web

#### Algoritmos Comuns de CSPRNG

**1. HMAC-DRBG (Baseado em HMAC)**
- Usa algoritmo HMAC (Hash-based Message Authentication Code)
- Gerencia estado duplo: chave K e valor pseudoaleatório V
- Maior resistência a ataques

**2. PRNG Baseado em SHA-256**
- Algoritmo hash SHA-256
- Não requer chaves adicionais
- Mecanismo mais simples, mas resistência a ataques inferior ao HMAC-DRBG

#### Geração de Sementes Aleatórias

O CSPRNG necessita de uma semente inicial de alta entropia:
- **Fontes de Sistema Operacional**: `/dev/urandom` (Linux), `CryptGenRandom` (Windows)
- **Hardware de Segurança**: HSM (Hardware Security Modules)
- **Número Verdadeiramente Aleatório (TRNG)**: Fontes verdadeiramente aleatórias do SO

#### Vantagem do CSPRNG sobre TRNG

O CSPRNG amplia a entropia disponível. Enquanto um TRNG é limitado pela capacidade do pool de entropia do sistema, o CSPRNG consegue gerar mais bits aleatórios quando necessário.

---

### AULA 02 - PRINCÍPIOS DE CRIPTOGRAFIA DE CHAVE PÚBLICA

#### Conceito Fundamental

A criptografia de chave pública (ou assimétrica) revolucionou a segurança em 1976 com Diffie e Hellman. Usa **dois pares de chaves distintas**: uma pública (divulgável) e uma privada (secreta).

#### Funcionamento Básico

```
Remetente recupera a chave pública do destinatário
          ↓
Remetente cifra mensagem com chave pública
          ↓
Mensagem é enviada criptografada
          ↓
Destinatário descriptografa com sua chave privada
          ↓
Somente quem tem a chave privada consegue descriptografar
```

#### Princípios Essenciais

1. **Confidencialidade**: Qualquer pessoa pode criptografar (usando chave pública), mas apenas o detentor da chave privada pode descriptografar
2. **Autenticação**: Criptografar com a chave privada e verificar com a pública prova identidade
3. **Não-repúdio**: Quem assinou com chave privada não pode negar assinatura

#### Vantagens da Criptografia Assimétrica

- **Eliminação do Problema de Troca de Chaves**: Não precisa compartilhar a chave de forma segura
- **Escalabilidade**: Funciona bem para muitos participantes
- **Auditabilidade**: Permite assinatura digital com validade jurídica
- **Infraestrutura de Chaves Públicas (PKI)**: Base para confiança digital

#### Desvantagens

- **Lentidão**: Computacionalmente intensiva (100 a 1000x mais lenta que simétrica)
- **Uso de Recursos**: Consumo significativo de processamento e memória
- **Tamanho de Dados**: Limitada a pequenos volumes de dados

#### Abordagem Híbrida (Padrão na Prática)

A indústria usa uma **combinação de ambos os métodos**:
1. Criptografia assimétrica distribui a chave de sessão
2. Criptografia simétrica criptografa os dados em volume
3. Resultado: Segurança + Eficiência

---

### AULA 03 - ALGORITMO RSA

#### O que é RSA?

**RSA (Rivest-Shamir-Adleman)** é o algoritmo assimétrico mais utilizado no mundo. Desenvolvido em 1977, baseia-se no problema matemático da fatoração de números grandes.

#### Fundamento Matemático

A segurança do RSA repousa em um princípio simples: é fácil multiplicar dois números primos grandes, mas é computacionalmente difícil fatorar o resultado.

```
Multiplicação Fácil:    p × q = n  (rápido)
Fatoração Difícil:      n = p × q  (muito lento)
```

#### Geração de Chaves RSA

**Processo passo a passo:**

1. **Seleção de Primos**: Escolher dois números primos grandes distintos (p e q)
   - Devem estar suficientemente afastados um do outro
   - Exemplo: p = 61, q = 53

2. **Cálculo de N**: n = p × q
   - Exemplo: n = 61 × 53 = 3.233

3. **Cálculo de φ(n)**: φ(n) = (p-1) × (q-1)
   - Função totiente de Euler
   - Exemplo: φ(3233) = 60 × 52 = 3.120

4. **Escolha de E**: Selecionar e tal que 1 < e < φ(n) e mdc(e, φ(n)) = 1
   - Comumente: e = 65.537
   - Exemplo: e = 17

5. **Cálculo de D**: Encontrar d tal que (e × d) mod φ(n) = 1
   - d é o inverso multiplicativo de e módulo φ(n)
   - Exemplo: d = 2.753

**Chave Pública**: (e, n)
**Chave Privada**: (d, n)

#### Processo de Criptografia

```
Mensagem M criptografada:
C = M^e mod n
```

#### Processo de Descriptografia

```
Mensagem descriptografada:
M = C^d mod n
```

#### Tamanhos de Chave RSA

| Tamanho | Aplicação | Segurança |
|---------|-----------|-----------|
| 512 bits | Obsoleto | Muito fraca |
| 1024 bits | Inadequado | Fraca |
| 2048 bits | Recomendado | Boa (até 2030) |
| 4096 bits | Alta Segurança | Excelente |

#### Segurança do RSA

**Baseada no Problema NP de Fatoração**

- O algoritmo mais rápido conhecido (NFS - Number Field Sieve) é exponencial
- Fatorar um número de 2048 bits levaria bilhões de anos com computadores atuais
- Ameaça: Computadores quânticos podem quebrar RSA em tempo polinomial

#### Limitações do RSA

- **Tamanho de Dados**: Mensagens devem ser menores que n
- **Velocidade**: Mais lento que criptografia simétrica
- **Padding Necessário**: Requer esquemas como OAEP para segurança

#### Aplicações do RSA

- Certificados digitais (X.509)
- Assinatura digital
- Distribuição segura de chaves
- Infraestrutura de Chaves Públicas (PKI)
- Protocolos TLS/SSL em HTTPS

---

### AULA 04 - PRETTY GOOD PRIVACY (PGP)

#### O que é PGP?

**Pretty Good Privacy** é um software de criptografia desenvolvido por Phil Zimmermann em 1991 que fornece autenticação, privacidade criptográfica e sigilo para comunicações digitais. É um sistema híbrido que combina criptografia simétrica e assimétrica.

#### Filosofia do PGP

- Privacidade como direito fundamental
- Resistiu a pressões governamentais desde a criação
- Operacionaliza a "Rede de Confiança" (Web of Trust) em vez de autoridades centralizadas

#### Arquitetura Híbrida do PGP

```
ENTRADA: Mensagem em Texto Simples
    ↓
[1] COMPRESSÃO: Reduz tamanho e aumenta segurança
    ↓
[2] GERAÇÃO DE CHAVE DE SESSÃO: Aleatória (usando CSPRNG)
    ↓
[3] CRIPTOGRAFIA SIMÉTRICA: Com chave de sessão (IDEA/AES-256)
    ↓
[4] CRIPTOGRAFIA ASSIMÉTRICA: Chave de sessão cifrada com chave pública do destinatário (RSA)
    ↓
SAÍDA: Dados cifrados + Chave de sessão criptografada
```

#### Funções de Criptografia no PGP

**Passo 1: Compressão**
- Reduz tamanho do arquivo
- Aumenta força criptográfica
- Remove padrões que criptanalistas exploram

**Passo 2: Geração de Chave de Sessão**
- Combinação de:
  - Movimentos aleatórios do mouse
  - Pressionamentos aleatórios do teclado
  - Teste de primalidade probabilístico
- Resulta em chave única para cada mensagem

**Passo 3: Encriptação Simétrica**
- Algoritmo: IDEA (International Data Encryption Algorithm)
- Alternativas modernas: AES-256
- Apenas Alice (remetente) e Bob (destinatário) têm a chave de sessão

**Passo 4: Encriptação da Chave de Sessão**
- RSA criptografa a chave de sessão
- Bob descriptografa com sua chave privada
- Depois descriptografa a mensagem com a chave de sessão

#### Assinatura Digital no PGP

```
ENTRADA: Mensagem
    ↓
CÁLCULO DE HASH: Resumo único da mensagem (SHA-1/SHA-256)
    ↓
ENCRIPTAÇÃO COM CHAVE PRIVADA: Cria assinatura
    ↓
SAÍDA: Mensagem + Assinatura Digital
    ↓
VERIFICAÇÃO (Bob):
    - Descriptografa assinatura com chave pública de Alice
    - Calcula hash da mensagem recebida
    - Compara hashes
    - Se iguais: Mensagem autêntica e íntegra
```

#### Recursos Principais do PGP

| Recurso | Função |
|---------|--------|
| **Confidencialidade** | Criptografia forte garante privacidade |
| **Autenticação** | Assinatura digital verifica identidade |
| **Integridade** | Detecção de alteração de mensagem |
| **Não-repúdio** | Impossível negar assinatura |
| **Compressão** | Reduz tamanho da transmissão |
| **Compatibilidade** | Padrão OpenPGP (RFC 4880) |

#### Rede de Confiança (Web of Trust)

**Diferente de Autoridades Certificadoras centralizadas:**
- Usuários atestam identidade uns dos outros
- Criação descentralizada de confiança
- Mais flexível, menos hierárquico
- Cada usuário tem "chave raiz de confiança"

#### Keyring (Chaveiro)

Arquivo local que contém:
- **Chave pública própria**
- **Chave privada própria** (criptografada com passphrase)
- **Chaves públicas de contatos** (com níveis de confiança)

#### Vantagens do PGP

- Forte segurança criptográfica (vários milhões de anos para quebrar)
- Decentralizado (sem dependência de autoridades)
- Auditado e aprovado pela comunidade criptográfica
- Compatível com padrões abertos

#### Limitações do PGP

- Complexidade de uso
- Gerenciamento de chaves pode ser confuso
- Problema de distribuição da chave pública inicial
- Interface não amigável em versões antigas

#### Aplicações Modernas

- Encriptação de e-mail
- Assinatura de softwares
- Proteção de dados sensíveis
- Comunicação entre jornalistas e fontes
- Ativismo digital e direitos humanos

---

### AULA 05 - TÓPICOS AVANÇADOS EM CRIPTOGRAFIA ASSIMÉTRICA

#### Variações e Melhorias de RSA

**RSASSA-PSS (Probabilistic Signature Scheme)**
- Adiciona elemento aleatório à assinatura
- Mais seguro que esquemas determinísticos
- Padrão recomendado (RFC 3447)

**OAEP (Optimal Asymmetric Encryption Padding)**
- Adiciona padding à mensagem antes de criptografar
- Melhora segurança semântica
- Impede ataques de criptoanálise

#### Alternativas ao RSA

**Criptografia de Curva Elíptica (ECC)**
- Baseada em propriedades de curvas algébricas
- Chaves menores que RSA (256 bits ECC ≈ 3072 bits RSA)
- Mais eficiente computacionalmente
- Futuro promissor em criptografia

**ECDSA (Elliptic Curve Digital Signature Algorithm)**
- Variante de assinatura de ECC
- Usado em Bitcoin e blockchain
- Menor tamanho de chave

**Diffie-Hellman**
- Protocolo de acordo de chave
- Não para criptografia, mas para estabelecer chave compartilhada
- Base para forward secrecy em TLS

#### Segurança em Longo Prazo

**Conceitos Importantes:**

1. **Post-Quantum Cryptography**: Algoritmos resistentes a ataques quânticos
   - Lattice-based cryptography
   - Hash-based signatures
   - Multivariate polynomial cryptography

2. **Compromisso de Forward Secrecy**: Mesmo se chave privada for comprometida, mensagens antigas permanecem seguras
   - Usado em TLS 1.3

3. **Key Rotation**: Renovação periódica de chaves

#### Ataques Comuns em Criptografia Assimétrica

**Ataque de Fatoração**
- Tentar fatorar n para recuperar p e q
- Mitigação: Usar primos grandes e bem espaçados

**Ataque de Timing**
- Analisa tempo de operação criptográfica
- Mitigação: Usar operações constantes em tempo

**Ataque de Força Bruta**
- Tentar todas as chaves possíveis
- Mitigação: Usar chaves suficientemente grandes

**Ataque de Lado de Canal**
- Explorar consumo de energia, emissões eletromagnéticas
- Mitigação: Blindagem física, contramedidas de software

---

### AULA 06 - ESTUDO DE CASO: MOEDAS DIGITAIS

#### O que são Moedas Digitais?

**Moedas Digitais (Criptomoedas)** são meios de troca gerenciados, armazenados ou trocados em ambiente digital, geralmente pela internet, utilizando criptografia para segurança.

#### Bitcoin: Caso de Uso Emblemático

**Componentes Criptográficos:**

1. **Hashing (SHA-256)**
   - Identifica blocos na blockchain
   - Prova de Trabalho
   - Imutabilidade de histórico

2. **Assinatura Digital (ECDSA)**
   - Verifica propriedade de moedas
   - Autoriza transferências
   - Não-repúdio de transações

3. **Chave Pública/Privada**
   - Chave privada = controle das moedas
   - Chave pública = endereço visível
   - Impossível falsificar transferências

#### Blockchain: Fundação Tecnológica

**Estrutura:**
```
[Bloco 1] → [Bloco 2] → [Bloco 3] → ... → [Bloco N]
  Hash0      Hash1       Hash2            HashN
  Dados0     Dados1      Dados2           DadosN
```

**Características de Segurança:**
- Lista encadeada de blocos
- Cada bloco vinculado ao anterior via hash
- Alteração de um bloco invalida toda a cadeia
- Descentralização: cópias em milhares de nós

#### Criptografia em Transações Bitcoin

**Processo de uma Transação:**

```
1. Alice prepara transação enviando Bitcoin para Bob
2. Transação é assinada com a chave privada de Alice (ECDSA)
3. Assinatura é verificada com a chave pública de Alice
4. Transação é propagada pela rede
5. Mineradores incluem em novo bloco
6. Bloco é validado por Proof of Work (computação intensiva)
7. Bloco é adicionado à blockchain
8. Transação é agora irreversível
```

#### Diferenças: Criptomoeda vs Moeda Digital

| Aspecto | Criptomoeda | Moeda Digital Centralizada |
|---------|------------|--------------------------|
| **Controle** | Descentralizado | Controlador centralizado |
| **Tecnologia** | Blockchain + Criptografia | Criptografia simples |
| **Segurança** | Muito alta (quebra difícil) | Alta (requer computador potente) |
| **Reversibilidade** | Quase impossível | Possível |
| **Exemplos** | Bitcoin, Ethereum | CBDC, Pix |

#### Desafios Criptográficos em Criptomoedas

1. **Perda de Chave Privada**: Bitcoin perdido para sempre
2. **Roubo de Chave**: Carteiras hackeadas
3. **Escalabilidade**: Blockchain Bitcoin: 7 transações/segundo
4. **Consumo de Energia**: Proof of Work é intensivo
5. **Privacidade**: Blockchain é transparente (pseudônimo, não anônimo)

#### Aplicações Futuras

- Smart Contracts com criptografia
- Zero-Knowledge Proofs
- Privacidade aprimorada (Monero, Zcash)
- Interoperabilidade entre blockchains

---

## UNIDADE 4 - CERTIFICAÇÃO DIGITAL

---

### AULA 01 - PRINCÍPIOS DE CERTIFICAÇÃO DIGITAL

#### O que é Certificação Digital?

**Certificação Digital** é um processo que usa criptografia para verificar e confirmar a identidade de pessoas ou entidades em transações digitais, garantindo autenticidade, confidencialidade e integridade.

#### Funcionamento Básico

```
PROCESSO DE CERTIFICAÇÃO:
    ↓
Usuário se identifica presencialmente
    ↓
Autoridade Certificadora verifica identidade
    ↓
AC gera par de chaves (pública/privada)
    ↓
AC emite certificado digital
    ↓
Usuário pode usar para assinar e autenticar
    ↓
Terceiros verificam autenticidade do certificado
```

#### Pilares da Certificação Digital

**1. Autenticação**
- Identidade do usuário é verificada
- Impossível falsificar identidade
- Credibilidade é garantida

**2. Integridade**
- Mensagens não podem ser alteradas
- Detecção automática de modificações
- Histórico de transações íntegro

**3. Confidencialidade**
- Dados são criptografados
- Acesso restrito aos autorizados
- Privacidade garantida

**4. Não-repúdio**
- Usuário não pode negar ação assinada
- Prova irrefutável de autoria
- Validade jurídica

#### Assinatura Digital vs Assinatura Eletrônica

| Aspecto | Assinatura Digital | Assinatura Eletrônica |
|--------|-------------------|----------------------|
| **Tecnologia** | Criptografia de chave pública | Qualquer método eletrônico |
| **Segurança** | Muito alta | Variável |
| **Validade Jurídica** | Plena (lei específica) | Plena em alguns casos |
| **Repúdio** | Impossível | Possível em alguns casos |
| **Exemplo** | Certificado ICP-Brasil | Clique em "Concordo" |

#### Vantagens da Certificação Digital

- Elimina necessidade de documento físico
- Acelera processos comerciais
- Reduz custos administrativos
- Aumenta segurança em transações
- Proporciona validade jurídica
- Facilita auditoria
- Possibilita assinatura remota

---

### AULA 02 - CERTIFICADO DIGITAL

#### O que é um Certificado Digital?

Um **Certificado Digital** é um documento eletrônico que vincula:
- A chave pública de um usuário
- Informações de identificação do usuário
- A assinatura digital da Autoridade Certificadora

É como um RG/CPF do mundo digital, emitido por autoridade confiável.

#### Estrutura de um Certificado Digital (X.509)

**Padrão Internacional: X.509v3**

```
CERTIFICADO X.509
├─ Versão: 3
├─ Número de série (único)
├─ Algoritmo de assinatura: sha256WithRSAEncryption
├─ Emissor: AC que emitiu
├─ Período de Validade
│  ├─ Válido a partir de: [data]
│  └─ Válido até: [data]
├─ Sujeito (Titular)
│  ├─ Nome Comum (CN)
│  ├─ Organização (O)
│  ├─ Unidade Organizacional (OU)
│  ├─ Localidade (L)
│  ├─ Estado (ST)
│  └─ País (C)
├─ Informações de Chave Pública
│  ├─ Algoritmo: RSA
│  └─ Chave Pública: [2048 bits]
├─ Extensões
│  ├─ Key Usage: Digital Signature, Non-Repudiation
│  ├─ Extended Key Usage: TLS Web Server Authentication
│  ├─ Subject Alternative Name: domínios alternativos
│  └─ Authority Key Identifier
└─ Assinatura da AC (valida integridade)
```

#### Componentes Críticos

**1. Nome Comum (CN)**
- Identifica principal: pessoa ou domínio
- Exemplo: "João Silva" ou "www.example.com"

**2. Período de Validade**
- Data de emissão e expiração
- Certificados A1: 1 ano
- Certificados A3: até 5 anos

**3. Chave Pública**
- Armazenada no certificado
- Usada para verificar assinatura

**4. Assinatura da AC**
- Garantia de autenticidade
- Verifica que AC realmente emitiu

#### Tipos de Certificados Digitais no Brasil

**Certificado A1**
- Validade: 1 ano
- Armazenamento: Arquivo no computador
- Fácil de copiar (backup)
- Mais vulnerável a roubo
- Recomendado para: Baixa segurança

**Certificado A3**
- Validade: até 5 anos
- Armazenamento: Token criptográfico ou cartão USB
- Deve estar conectado para usar
- Muito mais seguro
- Recomendado para: Alta segurança, autenticação bancária

**Certificado e-CPF**
- Pessoa física
- Identificação eletrônica
- Assinatura de documentos

**Certificado e-CNPJ**
- Pessoa jurídica
- Autenticação empresarial
- Assinatura de contratos

#### Ciclo de Vida de um Certificado

```
EMISSÃO
  ↓ (válido por 1-5 anos)
VIGÊNCIA
  ↓ (pode ser revogado)
REVOGAÇÃO ou EXPIRAÇÃO
  ↓
RENOVAÇÃO (novo certificado) ou FIM
```

#### Processo de Validação

**Quando alguém recebe certificado:**

```
1. Verifica assinatura da AC
2. Valida período de validade
3. Consulta CRL (Lista de Revogação)
4. Verifica cadeia até AC-Raiz
5. Se tudo OK → Certificado válido
```

---

### AULA 03 - AUTORIDADES CERTIFICADORAS

#### O que é uma Autoridade Certificadora?

Uma **Autoridade Certificadora (AC)** é uma entidade pública ou privada responsável por:
- Verificar identidade do solicitante
- Emitir certificados digitais
- Manter chaves privadas seguras
- Revogar certificados
- Manter lista de revogação

É o "cartório digital" do mundo digital.

#### Hierarquia de Autoridades Certificadoras

**Modelo Hierárquico (Brasil - ICP-Brasil):**

```
┌─────────────────────┐
│   AC-RAIZ (ITI)     │  (Ponto máximo de confiança)
│  (Instituto Nacional │
│ Tecnologia Inform.)  │
└──────────┬──────────┘
           │
      ┌────┴────┐
      ↓         ↓
┌──────────┐ ┌──────────┐
│AC NÍVEL 1│ │AC NÍVEL 1│  (ACs Intermediárias/Normativas)
│ (Exemplo)│ │ (Exemplo)│  (Credenciadas pela Raiz)
└────┬─────┘ └────┬─────┘
     │            │
  ┌──┴──┐      ┌──┴──┐
  ↓     ↓      ↓     ↓
┌──┐  ┌──┐   ┌──┐  ┌──┐
│AC│  │AC│   │AC│  │AC│   (ACs de Segundo Nível)
└──┘  └──┘   └──┘  └──┘   (Atendem usuários finais)
  │     │     │     │
  ↓     ↓     ↓     ↓
┌──────────────────┐
│ Usuários Finais  │    (Pessoas e empresas)
│ (Certificados)   │
└──────────────────┘
```

#### Estrutura da ICP-Brasil

**AC-Raiz** (Topo da Pirâmide)
- Instituto Nacional de Tecnologia da Informação (ITI)
- Define políticas e normas
- Emite certificados de ACs intermediárias
- Não emite para usuários finais
- Chave privada em sala-cofre de segurança máxima

**ACs Intermediárias de Primeiro Nível (Normativas)**
- Credenciadas pela AC-Raiz
- Emitem certificados para ACs de segundo nível
- Também em sala-cofre
- Exemplo: Serpro, Imprensa Oficial

**ACs de Segundo Nível**
- Atendem usuários finais
- Emitem certificados A1 e A3
- Responsáveis pela verificação de identidade
- Exemplo: Serasa Experian, Soluti

#### Responsabilidades de uma Autoridade Certificadora

**Emissão**
- Verificar identidade presencialmente
- Validar documentos
- Gerar chaves criptográficas
- Emitir certificado assinado

**Manutenção**
- Manter lista de revogação atualizada
- Armazenar certificados
- Gerenciar recursos
- Fazer backups

**Revogação**
- Cancelar certificados comprometidos
- Atualizar CRL (Certificate Revocation List)
- Emitir novo certificado

**Segurança**
- Proteger chave privada da AC
- Implementar controles de acesso
- Fazer auditoria
- Cumprir conformidade

#### Confiança em uma Autoridade Certificadora

**Critérios para Confiança:**

1. **Credenciamento**: Estar listada na AC-Raiz (para ICP-Brasil)
2. **Conformidade**: Seguir normas técnicas e operacionais
3. **Transparência**: Publicar Declaração de Práticas de Certificação (DPC)
4. **Auditoria**: Passar por auditorias independentes
5. **Responsabilidade**: Possuir seguros e garantias

**Modelo Web of Trust** (Alternativo)
- Descentralizado (PGP)
- Confiança em pares
- Sem autoridade central
- Menos formal, mas flexível

---

### AULA 04 - INFRAESTRUTURA DE CHAVES PÚBLICAS - BRASIL (ICP-BRASIL)

#### O que é ICP-Brasil?

A **Infraestrutura de Chaves Públicas Brasileira (ICP-Brasil)** é um sistema nacional hierárquico de confiança que viabiliza a emissão, distribuição e revogação de certificados digitais para identificação virtual no Brasil.

#### Criação e Regulamentação

**Marcos Legais:**
- **Medida Provisória 2.200-2 de 2001**: Criação oficial
- **Decreto 3.996 de 2001**: Regulamentação
- **Lei 11.419 de 2006**: Formalização de processo eletrônico

**Objetivo:** Garantir autenticidade, integridade e não-repúdio de documentos em transações eletrônicas.

#### Entes da Cadeia Hierárquica ICP-Brasil

**1. AC-Raiz (Autoridade Certificadora Raiz)**
- Executada pelo Instituto Nacional de Tecnologia da Informação (ITI)
- Primeira autoridade da cadeia
- Emite e gerencia certificados de ACs intermediárias
- Publica Lista de Certificados Revogados (LCR)
- Define normas técnicas e operacionais
- Subordinada ao Comitê Gestor da ICP-Brasil

**Principais Funções:**
- Emissão de certificados para ACs
- Auditoria de ACs
- Manutenção de políticas
- Revogação de certificados de ACs

**2. ACs Credenciadas (Intermediárias e de Segundo Nível)**
- Emitem certificados para usuários finais
- Devem cumprir normas do Comitê Gestor
- Submetem-se a auditorias regulares
- Exemplos:
  - Serpro (Serviço Federal de Processamento de Dados)
  - Imprensa Oficial do Estado de São Paulo
  - Serasa Experian
  - Soluti
  - ACT BRY

**Responsabilidades:**
- Verificar identidade do solicitante
- Emitir certificado
- Manter lista de revogação
- Responder por atos

**3. Comitê Gestor da ICP-Brasil**
- Órgão de supervisão política
- Define políticas de certificação
- Composto por representantes de governo, iniciativa privada e sociedade civil
- Aprova normas técnicas

**4. Autoridades Fiscalizadoras**
- Auditoram ACs
- Verificam conformidade
- Garantem qualidade
- Protegem consumidor

#### Funcionamento da ICP-Brasil

**Arquitetura:**
```
┌─────────────────────────────────┐
│  Comitê Gestor ICP-Brasil       │
│  (Define políticas)             │
└────────────┬────────────────────┘
             │
┌────────────▼──────────────────┐
│     AC-Raiz (ITI)             │
│ (Emite e audita ACs)          │
└────────────┬──────────────────┘
             │
      ┌──────┴─────┐
      ↓            ↓
 ┌────────┐    ┌────────┐
 │ AC Nível 1  │    │ AC Nível 1   │
 │(Serpro, etc)│    │ (Outro, etc) │
 └────────┬────┘    └────────┬─────┘
          │                  │
      ┌───┴──┐            ┌──┴───┐
      ↓      ↓            ↓      ↓
  ┌──────┐┌──────┐  ┌──────┐┌──────┐
  │AC 2º ││AC 2º │  │AC 2º ││AC 2º │
  │ Nível││ Nível│  │ Nível││ Nível│
  └──┬───┘└──┬───┘  └──┬───┘└──┬───┘
     │       │        │       │
     ↓       ↓        ↓       ↓
  [Usuários Finais com Certificados]
```

#### Padrões de Certificados ICP-Brasil

**Tipos de Certificados:**

1. **Certificado A1**
   - Validade: 1 ano
   - Armazenamento: Arquivo (com senha)
   - Uso: Pessoas e empresas
   - Vantagem: Portabilidade
   - Desvantagem: Menor segurança

2. **Certificado A3**
   - Validade: até 5 anos
   - Armazenamento: Token criptográfico
   - Uso: Alta segurança
   - Vantagem: Muito seguro
   - Desvantagem: Precisa de leitor

3. **Certificado A4** (Futuro)
   - Em desenvolvimento
   - Baseado em acesso remoto

**Tipos de Titulares:**

- **e-CPF**: Pessoa física
- **e-CNPJ**: Pessoa jurídica
- **Certificados de Poder de Autoridade**: Para órgãos públicos

#### Aplicações da ICP-Brasil

**Setor Público**
- Assinatura de processos administrativos
- Documentos eletrônicos
- Licitações e contratos
- Protocolos

**Setor Privado**
- Assinatura de contratos
- E-commerce
- Operações bancárias
- Medicina digital

**Documentos Eletrônicos**
- NFe (Nota Fiscal Eletrônica)
- RPA (Recibo de Pagamento Autônomo)
- Petições judiciais eletrônicas
- Documentos médicos

#### Benefícios da ICP-Brasil

- **Segurança**: Padrão de 2048 bits, criptografia forte
- **Validade Jurídica**: Reconhecida por lei
- **Interoperabilidade**: Aceita em órgãos governamentais
- **Confiabilidade**: Auditorias regulares
- **Rastreabilidade**: Auditoria completa de ações

---

### AULA 05 - TÓPICOS EM CERTIFICAÇÃO DIGITAL

#### Revogação de Certificados

**Por que Revogar?**
- Chave privada comprometida
- Usuário deixa a organização
- Dados do certificado desatualizados
- Certificado emitido por erro
- Fim da necessidade

**Processo de Revogação:**

```
Solicitação de revogação
    ↓
Verificação de identidade
    ↓
Confirmação de revogação
    ↓
Atualização de CRL
    ↓
Publicação em OCSP
    ↓
Certificado considerado inválido
```

**CRL (Certificate Revocation List)**
- Lista de certificados revogados
- Publicada periodicamente
- Baixada antes de usar certificado
- Lentidão: pode estar desatualizada

**OCSP (Online Certificate Status Protocol)**
- Consulta em tempo real
- Responde se certificado está revogado
- Mais rápido que CRL
- Padrão moderno

#### Validação e Verificação de Certificados

**Processo de Validação:**

```
1. Verifica assinatura da AC
   └─ Usa chave pública da AC

2. Valida período de vigência
   └─ Compara data atual com datas do certificado

3. Verifica cadeia de certificação
   └─ Valida certificado da AC que emitiu
   └─ Continua até AC-Raiz

4. Consulta status de revogação
   └─ CRL ou OCSP
   └─ Verifica se está revogado

5. Valida contra políticas locais
   └─ Tamanho de chave aceitável?
   └─ Algoritmo reconhecido?

Se TUDO OK → Certificado Válido ✓
```

#### Extensões de Certificado

**Campos Opcionais que adicionam Funcionalidades:**

**Key Usage**
- Digital Signature
- Non-Repudiation
- Key Encipherment
- Data Encipherment
- Key Agreement
- Key Certificate Sign
- CRL Sign
- Encipher Only
- Decipher Only

**Extended Key Usage**
- TLS Web Server Authentication
- TLS Web Client Authentication
- Code Signing
- Email Protection
- Time Stamping
- OCSP Signing

**Subject Alternative Name (SAN)**
- Domínios alternativos em certificado SSL/TLS
- Múltiplos domínios em um certificado
- Exemplo: *.example.com, www.example.com

**Authority Key Identifier**
- Identifica chave pública da AC que emitiu
- Facilita validação
- Evita ambiguidades

#### Certificado de Timestamp

**O que é?**
- Certificado que marca hora exata
- Prova que documento existia em determinada data/hora
- Não-repúdio temporal

**Aplicações:**
- Validade jurídica de documentos
- Contratos assinados eletronicamente
- Prova de anterioridade de propriedade intelectual
- Conformidade regulatória

---

### AULA 06 - ESTUDO DE CASO: SSL/TLS, OPENSSL E HEARTBLEED

#### O que é SSL/TLS?

**SSL (Secure Sockets Layer)** e **TLS (Transport Layer Security)** são protocolos criptográficos que garantem comunicação segura entre cliente e servidor na internet.

**Evolução:**
- SSL 2.0 (1995) → Obsoleto
- SSL 3.0 (1996) → Obsoleto
- TLS 1.0 (1999) → Legado
- TLS 1.1 (2006) → Legado
- TLS 1.2 (2008) → Atual
- TLS 1.3 (2018) → Moderno e Recomendado

#### Como Funciona SSL/TLS

**Handshake (Aperto de mão):**

```
1. CLIENT HELLO
   Cliente → Servidor
   - Versão TLS suportada
   - Cipher suites disponíveis
   - Número aleatório

2. SERVER HELLO
   Servidor → Cliente
   - Versão TLS escolhida
   - Cipher suite escolhida
   - Número aleatório

3. SERVER CERTIFICATE
   Servidor → Cliente
   - Certificado digital do servidor
   - Contém chave pública

4. SERVER KEY EXCHANGE (TLS 1.2)
   Servidor → Cliente
   - Parâmetros adicionais
   - Assinado com chave privada

5. CLIENT KEY EXCHANGE
   Cliente → Servidor
   - Pré-chave mestre criptografada
   - Com chave pública do servidor

6. CHANGE CIPHER SPEC
   Ambos
   - Comutação para modo seguro

7. FINISHED
   Ambos
   - Confirmação de sucesso
```

**Após Handshake:**
- Ambos possuem chave de sessão compartilhada (simétrica)
- Todos os dados criptografados com essa chave

#### Segurança do SSL/TLS

**Componentes de Segurança:**

1. **Confidencialidade**: Criptografia simétrica (AES)
2. **Integridade**: HMAC (hash com chave)
3. **Autenticação**: Certificado digital + assinatura
4. **Autenticação de Origem**: Certificado do servidor

#### OpenSSL

**O que é?**
- Implementação de código aberto de SSL/TLS
- Biblioteca de criptografia robusta
- Padrão da indústria
- Usado em servidores web, VPNs, email

**Funcionalidades:**
- Gerar chaves RSA
- Criar certificados digitais
- Estabelecer conexões TLS
- Verificar certificados
- Encriptar/desencriptar dados

**Versões Comuns:**
```
OpenSSL 1.0.2 (LTS)
OpenSSL 1.1.1 (LTS) ← Atual recomendado
OpenSSL 3.0 (Novo)
```

#### Vulnerabilidade Heartbleed (CVE-2014-0160)

**Data:** 7 de abril de 2014
**Severidade:** CRÍTICA (9.8/10)
**Versões Afetadas:** OpenSSL 1.0.1 até 1.0.1f

**O que é Heartbeat?**
- Extensão TLS que verifica se conexão ainda está ativa
- Cliente envia mensagem: "Olá, você está aí?"
- Servidor responde: "Sim, estou aqui"
- Mantém conexão viva

**Como Funciona o Exploit:**

```
COMUNICAÇÃO NORMAL:
Cliente envia:  [Dados] "Olá" [Tamanho: 4 bytes]
                           ↓
Servidor responde: "Olá"

EXPLOIT HEARTBLEED:
Cliente envia:  [Dados] "Olá" [Tamanho: 64.000 bytes]
                           ↓ (BUG!)
Servidor responde: "Olá" + [próximos 63.996 bytes da MEMÓRIA]
                           ↓
Atacante obtém: Chaves privadas, senhas, dados sensíveis, etc.
```

**Problema Técnico:**
- OpenSSL não validava corretamente tamanho do payload
- Servidor retornava quantidade de bytes solicitada
- Sem verificar se havia dados suficientes
- Resulta em vazamento de memória

**Dados Vazados Possíveis:**
- Chave privada do servidor (CRÍTICO!)
- Senhas de usuários
- Nomes de usuários
- Tokens de sessão
- Dados de clientes
- Qualquer coisa na memória do servidor

#### Impacto do Heartbleed

**Escala:** Afetou ~2 milhões de sites (17% da internet)
**Críticidade:** Considerado um dos piores bugs de segurança da história
**Publicação:** Descoberto por Neel Mehta (Google)

**Serviços Afetados:**
- Yahoo
- GitHub
- Tumblr
- OkCupid
- Dropbox
- Amazon (em alguns serviços)
- Muitos servidores de hospedagem

#### Mitigação e Resposta

**Imediato:**
1. Atualizar OpenSSL para versão 1.0.1g (patch)
2. Recompilar sem extensão Heartbeat
3. Revogar certificados comprometidos
4. Emitir novos certificados
5. Forçar troca de senhas de usuários

**OpenSSL 1.0.1g (Lançado 7/4/2014)**
- Validação corrigida de tamanho de payload
- Limite de tamanho máximo
- Verificação de limites

**Lições Aprendidas:**

1. **Importância de Auditoria de Código**: Bug estava escondido há 2 anos
2. **Testes de Segurança**: Fuzzing teria encontrado
3. **Responsável Disclosure**: Vulnerabilidade foi divulgada responsavelmente
4. **Atualização de Software**: Necessidade de patchear rapidamente
5. **Monitoramento**: Detectar vazamento de dados

#### Proteção Atual

**Mitigações Implementadas:**

1. **OpenSSL Moderno**: Versões seguras sem Heartbleed
2. **TLS 1.3**: Redesenho completo, mais seguro
3. **Perfect Forward Secrecy**: Chaves de sessão não comprometem histórico
4. **Certificate Pinning**: Cliente valida certificado específico
5. **HSTS**: Força HTTPS
6. **Monitoramento Contínuo**: Detecção de anormalidades

**Recomendações:**
- Manter OpenSSL atualizado
- Usar TLS 1.2 ou superior
- Implementar Perfect Forward Secrecy
- Fazer auditoria de segurança
- Aplicar patches promptamente

#### Lições para Certificação Digital

**A Importância da Confiança:**
- Certificados devem ser confiáveis
- Mas infraestrutura subjacente (software) também
- Segurança é um processo contínuo
- Vulnerabilidades acontecem
- Resposta rápida é crítica

---

## RESUMO EXECUTIVO PARA PROVA

### Conceitos-Chave da Unidade 3

1. **CSPRNG**: Geradores aleatórios resistentes a ataques, essenciais para chaves criptográficas
2. **Criptografia Assimétrica**: Usa par de chaves (pública/privada), soluciona problema de troca segura
3. **RSA**: Baseado em fatoração de primos, tamanho recomendado 2048 bits, padrão da indústria
4. **PGP**: Sistema híbrido, usa RSA para chave de sessão e simétrica para dados, autentica com assinatura digital
5. **Blockchain/Bitcoin**: Usa ECDSA (variante de ECC), hash SHA-256, imutabilidade através de encadeamento

### Conceitos-Chave da Unidade 4

1. **Certificado Digital**: Vincula chave pública à identidade, padrão X.509, emitido por AC
2. **Autoridade Certificadora**: Verifica identidade, emite e revoga certificados
3. **ICP-Brasil**: Hierarquia brasileira com AC-Raiz (ITI) no topo, normas governamentais
4. **SSL/TLS**: Protocolo para comunicação segura, TLS 1.3 recomendado
5. **Heartbleed**: Vulnerabilidade crítica em OpenSSL, vazava memória do servidor

### Questões Típicas de Prova

**"O que torna um CSPRNG diferente de um PRNG?"**
→ CSPRNG é resistente a ataques, irreversível, impede previsão de sequências, adequado para criptografia

**"Como funciona o RSA?"**
→ Gera dois primos grandes (p, q), calcula n=pq, escolhe e, calcula d, chave pública=(e,n), privada=(d,n), segurança baseada em dificuldade de fatoração

**"Por que PGP usa criptografia híbrida?"**
→ RSA é lento, então usa RSA apenas para criptografar chave de sessão, depois usa simétrica para dados (eficiente e seguro)

**"O que é certificado digital?"**
→ Documento eletrônico que vincula chave pública à identidade, emitido por AC, garante autenticidade e não-repúdio

**"Qual a diferença entre A1 e A3?"**
→ A1: 1 ano, arquivo (portável, menos seguro). A3: até 5 anos, token (seguro, precisa leitor)

**"O que é Heartbleed?"**
→ Bug em OpenSSL onde cliente solicitava mais dados que enviou, servidor retornava memória completa, vazando chaves privadas e dados sensíveis
