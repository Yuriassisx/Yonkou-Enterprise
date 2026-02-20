## Visão Geral

O YONKOU Aggressive Secret Scanner é um scanner avançado de alta performance desenvolvido para descobrir, coletar e analisar superfícies web com o objetivo de identificar secrets expostos, credenciais, tokens, chaves de API, endpoints sensíveis e configurações críticas.

<img width="1446" height="755" alt="image" src="https://github.com/user-attachments/assets/d4a51ff9-8736-4f1e-b459-239d7f5e52b0" />


O scanner utiliza múltiplas técnicas combinadas:

- Enumeração passiva e ativa
- Análise de conteúdo HTTP
- Detecção baseada em YARA e regex
- Análise de entropia
- Correlação de secrets
- Deduplicação persistente
- Scoring de severidade
- Execução concorrente em larga escala
- Pipeline completo de descoberta, coleta, análise e relatório


------------------------------------------------------------
ARQUITETURA GERAL
------------------------------------------------------------

Target Domain
     │
     ▼
Subdomain Discovery
     │
     ▼
URL Discovery
     │
     ▼
URL Queue
     │
     ▼
Concurrent Fetch Engine
     │
     ▼
Content Analysis Engine
     │
     ▼
Secret Detection Engine
     │
     ▼
Correlation Engine
     │
     ▼
Scoring Engine
     │
     ▼
Output Engine + Report


------------------------------------------------------------
FUNCIONALIDADES PRINCIPAIS
------------------------------------------------------------

1. Descoberta de Subdomínios

Utiliza subfinder para descobrir subdomínios associados ao domínio alvo.

Objetivos:

- Expandir superfície de ataque
- Identificar domínios expostos
- Mapear infraestrutura externa


------------------------------------------------------------

2. Descoberta de URLs

Coleta URLs usando múltiplas fontes:

- Coleta Massiva de Urls e Mirrors
- Wayback Machine API
- Enumeração ativa via wordlists

Objetivo:

- Maximizar cobertura de endpoints


------------------------------------------------------------

3. Sistema de Fila Global

Características:

- Fila thread-safe
- Deduplicação automática
- Normalização de URLs
- Persistência em disco
- Controle de crescimento

Evita:

- Reprocessamento
- Loops infinitos
- URLs duplicadas


------------------------------------------------------------

4. Engine de Fetch HTTP de Alta Performance

Características:

- Multithreading
- Requests simultâneos
- Retry automático
- Backoff exponencial
- Controle de concorrência via Semaphore
- Timeout configurável


------------------------------------------------------------

5. Sistema OPSEC

Funções:

- Randomização de User-Agent
- Simulação de navegador real
- Introdução de jitter
- Suporte a proxies
- Redução de detectabilidade


------------------------------------------------------------

6. Filtro Inteligente de Conteúdo

Ignora arquivos binários como:

.png
.jpg
.gif
.zip
.exe
.mp4
.pdf

Analisa apenas conteúdo relevante:

HTML
JSON
JavaScript
XML
GraphQL


------------------------------------------------------------

7. Engine de Detecção de Secrets

Utiliza múltiplas técnicas:


7.1 Detecção via YARA

Detecta:

- AWS Keys
- Google Keys
- Azure Secrets
- GitHub Tokens
- Slack Tokens
- Stripe Keys
- Twilio Keys
- Private Keys
- Connection strings


7.2 Detecção via Regex

Detecta:

- API Keys
- Tokens
- Credenciais hardcoded
- JWT
- Bearer tokens


7.3 Detecção via Entropia

Utiliza Shannon entropy para identificar secrets desconhecidos.


7.4 Decodificação Base64

Detecta secrets escondidos em Base64.


------------------------------------------------------------

8. Análise de Headers HTTP

Analisa headers como:

Authorization
Set-Cookie
X-API-Key
X-Auth-Token


------------------------------------------------------------

9. Enumeração de Superfície de API

Detecta endpoints sensíveis como:

/api
/admin
/auth
/config
/.env
/graphql
/swagger


------------------------------------------------------------

10. Sistema de Correlação

Cada secret recebe um fingerprint único baseado em:

secret + host

Permite:

- Deduplicação
- Correlação
- Rastreamento


------------------------------------------------------------

11. Sistema de Scoring

Classificação:

0–20    Low
21–40   Medium
41–70   High
71–100  Critical

Baseado em:

- Tipo
- Entropia
- Contexto
- Frequência


------------------------------------------------------------

12. Sistema Multithread

Utiliza ThreadPoolExecutor.

Capacidade:

- Alta concorrência
- Alto throughput


------------------------------------------------------------

13. Sistema de Deduplicação Persistente

Arquivo:

dedup.json

Evita reprocessamento.


------------------------------------------------------------

14. Sistema Realtime

Envia eventos para backend:

http://127.0.0.1:8000/internal/event

Inclui:

- URLs
- Secrets
- Métricas


------------------------------------------------------------

15. Sistema de Memória Persistente

Permite salvar:

- Histórico
- Secrets
- Correlações

Arquivo exemplo:

memory.json


------------------------------------------------------------

16. Geração de Relatórios

Suporte a exportação completa:

report.json

Inclui:

- Estatísticas
- Findings
- Histórico


------------------------------------------------------------

17. Sistema Anti-Kill

Inclui watchdog que:

- Mantém processo ativo
- Evita timeout
- Executa garbage collection


------------------------------------------------------------

18. Estrutura de Output

Cada finding inclui:

ID
Detection Type
Secret
URL
Entropy
Severity
Fingerprint
Correlation Count
Timestamp


------------------------------------------------------------

EXECUÇÃO
------------------------------------------------------------

Execução básica:

python yonkou.py -d example.com


Execução completa:

python yonkou.py -d example.com \
-o findings.txt \
--api-surface-enum \
--ext-score \
--ext-memory memory.json \
--ext-report report.json \
--ultra-verbose


------------------------------------------------------------

PERFORMANCE
------------------------------------------------------------

Capacidade:

- Milhares de URLs por minuto
- Alta concorrência
- Alta precisão
- Baixo overhead


------------------------------------------------------------

CASOS DE USO
------------------------------------------------------------

- Bug bounty
- Pentest
- Red Team
- Attack Surface Discovery
- Secret Discovery
- OSINT
- Security Research


------------------------------------------------------------

RESUMO FINAL
------------------------------------------------------------
O YONKOU é um scanner completo que combina:

- Discovery Engine
- Fetch Engine
- Analysis Engine
- Detection Engine
- Correlation Engine
- Scoring Engine
- Reporting Engine

em um pipeline altamente otimizado, escalável e focado em descoberta de secrets expostos.


# Contato
yuri.defciber@gmail.com

O YONKOU é um scanner completo que combina:

- Discovery Engine
- Fetch Engine
- Analysis Engine
- Detection Engine
- Correlation Engine
- Scoring Engine
- Reporting Engine

em um pipeline altamente otimizado, escalável e focado em descoberta de secrets expostos.
