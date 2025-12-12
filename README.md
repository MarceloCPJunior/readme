# Guia de Estudo — Criptografia, Certificados, Hashing, Autenticação e Protocolos

## 1. Conceitos Fundamentais

- Confidencialidade
  - Objetivo: impedir acesso não autorizado aos dados.
  - Ferramentas: criptografia (principalmente simétrica como AES).
- Integridade
  - Objetivo: garantir que os dados não foram alterados.
  - Ferramentas: funções hash (SHA-256), assinaturas digitais.
- Autenticidade
  - Objetivo: confirmar a identidade de quem envia/assina.
  - Ferramentas: certificados digitais, assinaturas (RSA/ECDSA).
- Não repúdio
  - Objetivo: impossibilitar que o autor negue a autoria.
  - Ferramentas: assinaturas digitais com certificados válidos.

## 2. Criptografia Simétrica vs Assimétrica

- Simétrica
  - Mesma chave para cifrar e decifrar.
  - Exemplos: AES, DES (antigo).
  - Vantagens: muito rápida; ideal para grandes volumes.
  - Desafios: distribuição segura da chave.
- Assimétrica
  - Par de chaves: pública (compartilhável) e privada (secreta).
  - Exemplos: RSA, ECDSA (assinatura).
  - Vantagens: não requer compartilhar a chave privada; facilita troca inicial de segredos e verificação de assinaturas.
  - Desvantagens: mais lenta que a simétrica para cifrar grandes volumes.
- Característica-chave da assimétrica: envolve pares de chaves públicas e privadas.

## 3. Hashing

- Função unidirecional que gera um resumo (hash) de tamanho fixo.
- Não cifra nem decifra; serve para integridade e armazenamento de senhas (com sal).
- Propriedades desejadas: resistência a colisão e a pré-imagem.
- Exemplo: SHA-256.
- Uso típico: verificar se o conteúdo foi alterado comparando hashes.

## 4. Assinatura Digital e Certificados

- Assinatura Digital
  - Garante integridade, autenticidade e não repúdio.
  - Feita com a chave privada do titular; verificada com a chave pública.
  - Exemplos: RSA, ECDSA.
- Certificado Digital (conceito)
  - Documento eletrônico que associa uma chave pública a uma entidade (pessoa/sistema/empresa).
  - Contém dados do titular, chave pública, validade, assinatura da Autoridade Certificadora (AC).
  - Verificação de certificado: confirma validade e cadeia de confiança (PKI).
- PKI (Infraestrutura de Chaves Públicas)
  - Gerenciamento de certificados: emissão, validação, revogação.
  - Componentes: Autoridade Certificadora (CA), registro, listas de revogação/OCSP.

## 5. Tipos/Modos de Cifra

- Criptografia de bloco
  - Opera em blocos fixos de dados.
  - Exemplo: AES (modos CBC, GCM, CTR).
- Criptografia de fluxo
  - Cifra dados de forma contínua (bit/byte a bit/byte).
  - Útil para fluxos e baixa latência.

## 6. Troca de Chaves

- Diffie-Hellman (DH) / ECDH
  - Acordo seguro de chave sobre canal inseguro.
  - Base para PFS (Perfect Forward Secrecy) em TLS.
  - Correção comum: DH não é “pseudônimo”; é protocolo de troca de chaves.

## 7. Protocolos e Aplicações

- TLS/SSL
  - Protocolo que provê confidencialidade, integridade e autenticidade na internet (HTTPS, SMTPS).
  - Usa certificados e criptografia híbrida (assimétrica para negociar chaves, simétrica para dados).
- VPN
  - Conexão segura remota por túnel criptografado.
- Blockchain
  - Segurança e integridade de transações por estruturas encadeadas e funções criptográficas.
- SMTP
  - Protocolo de e-mail; não garante segurança por si só.
  - Segurança é adicionada via STARTTLS/TLS (SMTPS).
- HTTP/FTP
  - Protocolos sem segurança nativa; suas versões seguras usam TLS (HTTPS, FTPS).

## 8. Correções Típicas de Prova (base nas questões vistas)

- Função principal da criptografia em SI: proteger a confidencialidade dos dados.
- Vantagem da assimétrica sobre a simétrica: não requer compartilhar a chave privada; evita compartilhar um único segredo.
- Correspondências:
  - AES → criptografia simétrica.
  - RSA → criptografia assimétrica.
  - ECDSA → algoritmo de assinatura digital (assimétrico).
  - SHA-256 → função hash.
  - Diffie-Hellman → troca de chaves.
- Termos:
  - Chave pública → disponível para todos.
  - Chave privada → mantida em segredo.
  - Criptografia de fluxo → cifra continuamente.
  - Criptografia de bloco → cifra em blocos fixos.
- Certificado digital (definição correta):
  - Documento eletrônico que associa uma chave pública a uma entidade.
- Autenticação (objetivo):
  - Verificar a identidade de usuários.
- Segurança de comunicações na internet:
  - Protocolo correto: TLS.

## 9. Fluxo Típico de Comunicação Segura

1. Cliente inicia conexão segura (ex.: HTTPS).
2. Servidor apresenta certificado (cadeia assinada por CA confiável).
3. Cliente verifica validade do certificado (data, CA, revogação).
4. Troca/negociação de chaves (DH/ECDH) para estabelecer chave simétrica de sessão.
5. Dados são cifrados usando AES (modo seguro como GCM).
6. Integridade assegurada por MAC/AEAD; autenticidade por certificado.

## 10. Dicas Rápidas de Memorização

- Mapas mentais:
  - AES/Simétrica/Rápida/Grandes volumes.
  - RSA/ECDSA/Assimétrica/Assinatura/Chaves par.
  - SHA-256/Hash/Integridade/Senhas+sal.
  - DH/ECDH/Troca de chaves/PFS.
- Protocolos:
  - TLS = segurança; SMTP/HTTP/FTP precisam de TLS para segurança.
- Certificados:
  - Ligam identidade à chave pública; verificação = PKI.

## 11. Perguntas de Revisão

- Explique a diferença entre confidencialidade e integridade.
- Por que a criptografia assimétrica é útil para troca de chaves?
- O que torna o hashing adequado para verificar integridade?
- Qual o papel do certificado digital em TLS?
- Diferencie cifras de bloco e de fluxo.
- Quando usar AES vs RSA?
- Como o Diffie-Hellman contribui para PFS?

## 12. Referências Sugeridas

- NIST SP 800-57 e SP 800-38 (modos de operação de cifras de bloco).
- RFC 5280 (PKI e certificados X.509).
- RFCs de TLS (RFC 8446 — TLS 1.3).
- OWASP Cryptographic Cheat Sheet.
