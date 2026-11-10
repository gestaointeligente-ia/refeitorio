# 🛡️ Refeitório Inteligente B2B — Auditoria Biométrica, Prevenção de Glosas & IA Operacional

> **De uma dor real no chão de fábrica em Candeias-BA para um SaaS B2B Full-Cloud de nível Enterprise.**  
> Desenvolvido por **Ricardo Silva Lima** como vitrine técnica e de Produto para o programa **Estágio iFood GenAI (Trilha AI Builder / Produto & Impacto)**.

---

## 🎯 1. O Problema Real (Product Discovery)

Durante quase 2 anos operando a rotina administrativa e de faturamento da **Sodexo** dentro do complexo industrial da **Ultragaz (Mataripe/Candeias-BA)** — atendendo simultaneamente mais de **10 empresas consorciadas** (Ultragaz, Soservi, Armac, SegurPro, AVI Segurança, BC Transportes, JC Montagem, Top Service, Predial, entre outras) — identifiquei um gargalo crítico que custava dezenas de horas mensais e gerava risco direto de perda de receita (**glosas contratuais**):

1. **Dupla Batida e Reflexo de Catraca (Control iD):** Colaboradores passavam o crachá duas vezes no mesmo turno (por reflexo de giro da catraca em $\Delta \le 60\text{s}$ ou repasse indevido de crachá em $\Delta > 60\text{s}$), inflando artificialmente os lotes `.CSV` brutos e gerando contestação de faturas.
2. **Complexidade de Precificação Multi-Contrato (SLA):** Tarifas distintas entre a empresa-mãe (**Ultragaz**) e o **Consórcio de Parceiros**, somadas a tarifas especiais em **Datas Festivas / Aniversariantes do Mês** (calculadas automaticamente no último dia útil do mês) e acessos **Fora da Janela de Escala (SLA)**.
3. **Atrito na Conciliação Financeira:** O fechamento exigia cruzar milhares de linhas `.CSV` em Tabelas Dinâmicas no Excel com vouchers físicos de portaria (motoristas/visitantes) e ajustes contratuais (Coffee Breaks e Glosas).

**A Solução:** Construí o **Refeitório Inteligente**, uma plataforma SaaS B2B que transforma o arquivo `.CSV` bruto do leitor biométrico Control iD em um **Cockpit Financeiro e Operacional Auditado em Tempo Real**, com emissão de Boletins de Medição em PDF selados criptograficamente (`SHA-256`) e planilhas executivas `.XLSX` em 3 abas.

---

## 🚀 2. Acesso Fast-Track para Avaliadores iFood (1-Click Sandbox)

Para eliminar qualquer fricção de criação de conta ou configuração de banco durante a avaliação técnica, a tela de login possui o portal exclusivo **"Sandbox Avaliador iFood GenAI (Fast-Track 1-Click)"**:

- **Zero Senha:** Autentica instantaneamente na operação real auditada de **Julho/2025** ($1.926$ refeições validadas).
- **Gerador de Lote CSV Demo In-App:** Na gaveta **Entrada de Dados**, o avaliador pode baixar com 1 clique um lote `.CSV` realístico de **Junho/2025** (30 acessos com duplicidades intencionais e batidas fora de horário), importar para a nuvem Supabase e testar o **Protocolo de Rollback** instantâneo.

---

## 🧠 3. Arquitetura de Produto & Engenharia de Dados (ADRs)

### 🔹 ADR-01: Firewall de Idempotência & Laudo Anti-Fraude em PDF
- Na ingestão do lote `.CSV` (`ISO-8859-1`), o motor sanitiza cada registro combinando `Colaborador + Data + Turno/Faixa Horária`.
- Batidas duplicadas são bloqueadas antes de chegarem ao banco de dados.
- **Diagnóstico Automático por Delta Temporal ($\Delta t$):** O sistema emite um **Laudo Nominal de Duplicidades em PDF** que calcula em Reais ($\text{R\$}$) a **Glosa Evitada** e classifica cada retenção:
  - $\Delta t \le 60\text{s} \rightarrow$ **Reflexo de Leitor / Giro de Catraca** (Erro operacional sem dolo).
  - $\Delta t > 60\text{s} \rightarrow$ **Alerta de Repasse de Crachá / 2ª Fila** (Auditoria disciplinar).

### 🔹 ADR-02: Zero-Hallucination Financial AI Engine (120 FPS Edge Heuristics)
- Em sistemas financeiros B2B auditados, uma alucinação numérica de um LLM generativo no cálculo de uma fatura destrói a confiança do cliente.
- O motor **Forecast AI** utiliza **Heurística Determinística de Baixa Latência no Front-End**, garantindo **0% de alucinação matemática**, proteção de chaves de API e resposta instantânea:
  - **Projeção Run-Rate ($22\text{ dias úteis}$):** Em lotes parciais, projeta o fechamento mensal ponderando a média diária real mais o saldo de adicionais/glosas.
  - **Telemetria de Gargalo de Rampa:** Identifica o minuto exato de maior pressão na catraca (acessos/minuto) e sugere ações preventivas (ex: antecipação de abertura da 2ª rampa em $15\text{ min}$ para redução de fila em $\approx 38\%$).
  - **Modo Spotlight (`📈 VER RAMPA`):** Isola visualmente a curva de tráfego, os KPIs de topo e o parecer da IA para uma única empresa parceira com 1 clique.

### 🔹 ADR-03: Tarifação Proporcional por Proximidade Temporal & Tolerância SLA
- **Vista Grossa Operacional Configurável:** O gestor alterna em tempo real entre `0 min` (horário 100% estrito), `-15 min` (abertura antecipada da rampa) ou `+15 min` (atraso pós-fechamento).
- **Zero Descarte Financeiro:** Acessos fora da janela de SLA recebem flag de auditoria (`⚠️ Fora do Horário`), mas são tarifados proporcionalmente pela faixa horária correspondente (Manhã/Desjejum, Almoço, Tarde/Lanche, Noite/Jantar) de acordo com o contrato da empresa e o calendário do dia (Normal vs. Evento).
- **Cálculo de Ticket Médio Ponderado:** Simulador instantâneo baseado na matriz operacional de $22\text{ dias úteis}$ ($21\text{d Normais} + 1\text{d Evento}$) com pesos de $50\%$ Almoço, $25\%$ Desjejum, $15\%$ Lanche e $10\%$ Jantar.

### 🔹 ADR-04: Simetria Tripla & Livro-Razão Imutável (Append-Only Ledger)
- **Conciliação 100% Exata (`Dashboard === PDF === Excel`):** Tratamento rigoroso de ponto flutuante (`Math.round(val * 100) / 100`) e blindagem de fuso horário fixo `BRT (-03:00)` (imune a servidores `UTC` ou VPN).
- **Cofre Criptográfico (`#modal-cofre`):** Cada fatura emitida gera um selo `SHA-256` com timestamp hexadecimal embutido, ficando armazenada de forma imutável na nuvem com busca instantânea e filtro por calendário.

---

## 🛠️ 4. Stack Tecnológica

| Camada | Tecnologias Utilizadas |
| :--- | :--- |
| **Front-End & UI** | HTML5 Semântico, CSS3 Custom Properties (Glassmorphism / 120 FPS GPU Accelerated), Vanilla JavaScript (ES6+) |
| **Banco de Dados & Cloud** | **Supabase (PostgreSQL)** — Persistência em tempo real nas tabelas `refeicoes`, `contratos_b2b`, `fluxo_caixa_avulso`, `base_conhecimento`, `faturas_cofre` e `configuracoes_gerais` |
| **Visualização & Datas** | **Chart.js** (Curvas de Rampa Dinâmicas) + **Flatpickr** (Calendário Dark Mode com Máscara Dinâmica) |
| **Motores de Exportação** | **html2pdf.js** (Paginação Dinâmica Inteligente A4) + **SheetJS / XLSX** (Compilador de Planilhas Multi-Abas Formatadas) |
| **Metodologia de Build** | **Vibe Coding & Product-Led Engineering** — Prototipação assistida por IA guiada por regras reais de domínio B2B e auditoria matemática rigorosa |

---

## 👨‍💻 Autor

**Ricardo Silva Lima**  
Graduando em Administração | Analista de Suporte SaaS/ERP & AI Product Builder  
📍 Candeias, Bahia, Brasil  
📧 ricardosilvax86@gmail.com | 📱 (71) 98603-0162