# 🍽️ Refeitório Inteligente B2B | Sandbox Operacional

![Status](https://img.shields.io/badge/Status-Concluído_|_Pronto_para_Auditoria-success)
![Stack](https://img.shields.io/badge/Stack-HTML5_|_CSS3_|_JavaScript_ES6+-f3df49)
![Foco](https://img.shields.io/badge/Foco-Product_Management_|_AI_Builder-ff69b4)

> **Um projeto desenvolvido por Ricardo Lima.**

## 🎯 O Problema (Dor Real do Cliente B2B)
Durante minha experiência em operações B2B na **Sodexo (unidade Ultragaz)**, identifiquei um gargalo financeiro e operacional crítico: o fechamento mensal de faturamento do refeitório (auditado via catracas físicas *Control iD*) era feito através de planilhas manuais. 

Isso gerava:
- **Glosas financeiras** devido a batidas duplicadas (reflexo de leitor ou erro humano).
- **Falta de visibilidade** sobre gargalos de fila nos horários de pico (prejudicando o tempo de descanso dos trabalhadores operacionais no chão de fábrica).
- **Desperdício de horas** do setor administrativo consolidando centavos e regras de tolerância.

## 🚀 A Solução
O **Refeitório Inteligente** é um SaaS web *offline-first* (baseado em processamento em lote/CSV) que atua como um **Firewall de Auditoria**. Ele ingere os logs brutos da catraca, higieniza os dados com regras de negócio complexas e emite laudos invioláveis.

### 💡 Por que via CSV (Batch) e não em Tempo Real (API)?
A escolha arquitetural por Ingestão de Arquivo em vez de Webhooks em tempo real foi **estratégica** focando na resiliência de ambientes industriais (OT vs. IT):
1. **Segurança (Air-Gap):** Catracas de polos petroquímicos operam em redes isoladas (VLAN) por normas rígidas de segurança cibernética e patrimonial.
2. **Resiliência:** Se a internet oscilar às 12h00, a catraca não pode travar a fila aguardando resposta da nuvem.
3. **Idempotência & Curadoria:** O processamento em lote permite simular regras de tolerância (`-15m / +15m`) e gerar relatórios de duplicidades antes de efetivar a cobrança financeira (Evitando *Rollbacks* complexos).

## ✨ Funcionalidades Principais (Core Features)
- **Fast-Track Sandbox (1-Click):** Botão injetado para recrutadores/avaliadores carregarem uma massa de dados fictícia em 1 segundo e testarem a plataforma sem precisarem buscar arquivos locais.
- **Motor de Regras SLA:** Aplicação dinâmica de tolerâncias de horário (Antes/Depois) e isolamento de batidas atípicas ("Fora de Faixa").
- **Proteção Contra Duplicidade (Anti-Glosa):** Algoritmo que detecta e neutraliza marcações do mesmo funcionário com $\Delta \le 60$ segundos.
- **Modo Spotlight (Visão de Rampa):** Gráfico de calor analítico que identifica os horários de maior gargalo na fila, minuto a minuto.
- **Exportação Criptográfica:** Geração de Fatura PDF com validação hash `SHA-256`, garantindo compliance e rastreabilidade para o cliente final.

## 🛠️ Como Testar (Deploy)
Acesse a aplicação rodando ao vivo, sem precisar instalar nada:
🔗 **[Inserir seu link da Vercel aqui, ex: https://refeitorio-b2b.vercel.app]**

*Para avaliar o projeto:*
1. Acesse o link acima.
2. Clique no botão vermelho **"Sandbox Avaliador iFood"** na tela inicial.
3. Navegue pelo Dashboard, explore o modo *Spotlight* no gráfico e teste as exportações em PDF/Excel.

## 🧑‍💻 Autor
**Ricardo Silva Lima**
- [LinkedIn](INSERIR_LINK_AQUI)
- Focado em automação, eficiência B2B e democratização do impacto social através da tecnologia.
