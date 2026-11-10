# 🍽️ Refeitório Inteligente B2B | Auditoria e Fluxo de Refeições

![Status](https://img.shields.io/badge/Status-Concluído_|_Pronto_para_Auditoria-success)
![Stack](https://img.shields.io/badge/Stack-HTML5_|_CSS3_|_JavaScript_ES6+-f3df49)
![Foco](https://img.shields.io/badge/Foco-Product_Management_|_AI_Builder-ff69b4)

> **Um projeto desenvolvido por Ricardo Lima. De uma dor real em Mataripe-BA para um SaaS B2B Full-Cloud de nível Enterprise.**

> 🎬 **[Clique aqui para assistir à Apresentação e Demonstração do Produto em 90s](COLE_O_LINK_DO_SEU_VIDEO_AQUI)**

## 🎯 O Problema (Dor Real do Cliente B2B)
Durante minha experiência em operações B2B na **Sodexo (Operação Ultragaz)**, identifiquei um gargalo financeiro e operacional crítico: o fechamento mensal de faturamento do refeitório (auditado via catracas físicas *Control iD*) era feito através de planilhas manuais. 

Isso gerava:
- **Glosas financeiras** devido a batidas duplicadas (reflexo de leitor ou erro humano).
- **Falta de visibilidade** sobre gargalos de fila nos horários de pico (prejudicando o tempo de descanso dos trabalhadores operacionais no chão de fábrica).
- **Desperdício de horas** do setor administrativo consolidando centavos e regras de tolerância.
- **Atrito na Conciliação Financeira:** O fechamento exigia cruzar milhares de linhas .CSV em Tabelas Dinâmicas no Excel com tickets físicos de motoristas e ajustes contratuais (Coffee Breaks e Glosas).

## 🚀 A Solução
O **Refeitório Inteligente** é um SaaS web *offline-first* (baseado em processamento em lote/CSV) que atua como um **Firewall de Auditoria**. Ele ingere os logs brutos da catraca, higieniza os dados com regras de negócio complexas e emite laudos invioláveis.

### 💡 Por que via CSV e não em Tempo Real (API)?
A escolha arquitetural por Ingestão de Arquivo em vez de Webhooks em tempo real foi **estratégica** focando na resiliência de ambientes industriais:
1. Catracas de polos petroquímicos operam em redes isoladas (VLAN) por normas rígidas de segurança cibernética e patrimonial.
2. Se a internet oscilar às 12h00, a catraca não pode travar a fila aguardando resposta da nuvem.
3. O processamento em lote permite simular regras de tolerância (`-15m / +15m`) e gerar relatórios de duplicidades antes de efetivar a cobrança financeira (Evitando *Rollbacks* complexos).

## ✨ Funcionalidades Principais (Core Features)
- **Fast-Track Sandbox (1-Click):** Botão injetado para recrutadores/avaliadores carregarem uma massa de dados fictícia em 1 segundo e testarem a plataforma sem precisarem buscar arquivos locais.
- **Motor de Regras SLA:** Aplicação dinâmica de tolerâncias de horário (Antes/Depois) e isolamento de batidas atípicas ("Fora de Faixa").
- **Proteção Contra Duplicidade (Anti-Glosa):** Algoritmo que detecta e neutraliza marcações do mesmo funcionário com $\Delta \le 60$ segundos.
- **Modo Spotlight (Visão de Rampa):** Gráfico de calor analítico que identifica os horários de maior gargalo na fila, minuto a minuto. Isola visualmente a curva de tráfego, os KPIs de topo e o parecer da IA para uma única empresa parceira com 1 clique.
- **Exportação Criptográfica:** Geração de Fatura PDF com validação hash `SHA-256`, garantindo compliance e rastreabilidade para o cliente final.
- **Zero Descarte Financeiro:** Acessos fora da janela de SLA recebem flag de auditoria (`⚠️ Fora do Horário`), mas são tarifados proporcionalmente pela faixa horária correspondente (Manhã/Desjejum, Almoço, Tarde/Lanche, Noite/Jantar) de acordo com o contrato da empresa e o calendário do dia (Normal vs. Evento).
- **Cálculo de Ticket Médio Ponderado:** Simulador instantâneo baseado na matriz operacional de $22\text{ dias úteis}$ ($21\text{d Normais} + 1\text{d Evento}$) com pesos de $50\%$ Almoço, $25\%$ Desjejum, $15\%$ Lanche e $10\%$ Jantar.

## 🛠️ Como Testar (Deploy)
Acesse a aplicação rodando ao vivo, sem precisar instalar nada:
🔗 **https://github.com/gestaointeligente-ia/refeitorio.git**

*Para avaliar o projeto:*
1. Acesse o link acima.
2. Clique no botão vermelho **"Sandbox Avaliador iFood"** na tela inicial (não exige senha).
3. Navegue pelo Dashboard, explore o modo *Spotlight* no gráfico e teste as exportações em PDF/Excel.

## 👨‍💻 Autor

**Ricardo Silva Lima**  
*Gestão de Processos & Conformidade B2B | Otimização Operacional | Graduando em Administração*  

📍 Salvador, Bahia, Brasil  

> *"Focado em automação, eficiência B2B e democratização do impacto social através da tecnologia."*

[![LinkedIn](https://img.shields.io/badge/LinkedIn-0077B5?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/ricardo-lima-a29240225/)
[![Email](https://img.shields.io/badge/Email-D14836?style=for-the-badge&logo=gmail&logoColor=white)](mailto:ricardosilvax86@gmail.com)
[![WhatsApp](https://img.shields.io/badge/WhatsApp-25D366?style=for-the-badge&logo=whatsapp&logoColor=white)](https://wa.me/5571986030162)
  <a href="https://raw.githubusercontent.com/gestaointeligente-ia/refeitorio/main/curr%C3%ADculo_Ricardo_Lima-rev10" download="Curriculo_Ricardo_Lima.pdf" target="_blank">
    <img src="https://img.shields.io/badge/CURR%C3%8DCULO-BAIXAR_PDF-FFD700?style=for-the-badge&logo=adobe-acrobat-reader&logoColor=black&labelColor=FFA500" alt="Baixar Currículo" />
  </a>
