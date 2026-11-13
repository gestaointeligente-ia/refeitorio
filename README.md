# 🍽️ Refeitório Inteligente B2B | Auditoria e Fluxo de Refeições

![Status](https://img.shields.io/badge/Status-Concluído_|_Pronto_para_Auditoria-success)
![Stack](https://img.shields.io/badge/Stack-HTML5_|_CSS3_|_JavaScript_ES6+-f3df49)
![Foco](https://img.shields.io/badge/Foco-Product_Management_|_AI_Builder-ff69b4)

> **Um projeto desenvolvido por Ricardo Lima. De uma dor real em Mataripe-BA para um SaaS B2B Full-Cloud de nível Enterprise.**
> **Conciliação Financeira, Auditoria de SLA e Inteligência Operacional para Refeitórios Industriais (Integração Control iD).**

[![Video Pitch](https://img.shields.io/badge/▶️_ASSISTIR_DEMO_RÁPIDA-Vídeo_de_2_Minutos-3b82f6?style=for-the-badge)](https://SEU-LINK-DO-VIDEO-AQUI)

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

| Módulo | Entrega de Produto & Regra de Negócio | Impacto B2B |
| :--- | :--- | :--- |
| **🛡️ Firewall de Idempotência (Control iD)** | Filtra batidas repetidas do mesmo colaborador no mesmo turno e diagnostica o delta: $\Delta \le 60\text{s}$ = **Reflexo de Catraca** vs. $\Delta > 60\text{s}$ = **Alerta de Repasse de Crachá**. | Elimina 100% das cobranças em duplicidade e quantifica a **Glosa Evitada (R$)** no PDF. |
| **⚙️ Motor de Precificação 4XL & Tolerância SLA** | Configuração em nuvem de tarifas (*Ultragaz* vs. *Parceiros*, *Dias Normais* vs. *Aniversariantes*), Data Festiva automática (último dia útil) e botões de tolerância (`0 min`, `-15 min`, `+15 min`). | **Tarifação Proporcional por Proximidade:** Acessos fora de janela geram alerta de *Atípico*, mas são cobrados pelo turno contratual mais próximo. |
| **📈 Modo Spotlight & Forecast AI** | Gráfico de calor analítico que identifica os horários de maior gargalo na fila, minuto a minuto, com recomendação de escalonamento de rampa. Isola visualmente a curva de tráfego, os KPIs de topo e o parecer da IA para uma única empresa parceira com 1 clique. | Previsibilidade de caixa para o gestor e redução de filas físicas no refeitório. |
| **📑 Exportação Tripla & Cofre SHA-256** | Geração de Boletim PDF com paginação dinâmica anti-corte, Lote `.ZIP` individual por empresa, Excel `.XLSX` com 3 abas executivas e Cofre de Faturas com hash SHA-256,  | Rastreabilidade jurídica e contábil ponta a ponta entre Sodexo, Ultragaz e terceirizadas. |
| **🤝 Gestão de Contratos B2B & Documentos** | Controle de vigência contratual (*Ativos*, *Vence em 30d*, *Vencidos*), preview nativo de múltiplos PDFs em Base64 e repositório de *Compliance Legal (NR-20 / ISO 22000)*. | Centralização de governança legal e operacional em uma única interface. |

Além disso, contamos com:
- **Zero Descarte Financeiro:** Acessos fora da janela de SLA recebem flag de auditoria (`⚠️ Fora do Horário`), mas são tarifados proporcionalmente pela faixa horária correspondente (Manhã/Desjejum, Almoço, Tarde/Lanche, Noite/Jantar) de acordo com o contrato da empresa e o calendário do dia (Normal vs. Evento).
- **Cálculo de Ticket Médio Ponderado:** Simulador instantâneo baseado na matriz operacional de $22\text{ dias úteis}$ ($21\text{d Normais} + 1\text{d Evento}$) com pesos de $50\%$ Almoço, $25\%$ Desjejum, $15\%$ Lanche e $10\%$ Jantar.

## 🛠️ Como Testar (Deploy)
Acesse a aplicação rodando ao vivo, sem precisar instalar nada:

[![Live Demo](https://img.shields.io/badge/🚀_ACESSAR_SISTEMA-Sandbox_1--Click_iFood-EA1D2C?style=for-the-badge)](https://gestaointeligente-ia.github.io/refeitorio/)

*Para avaliar o projeto, o sistema conta com um Fast-Track VIP na tela de login:* 
1. Acesse o link acima.
2. Clique no botão vermelho **"Avaliador iFood GenAI"** na tela inicial (não exige senha).
3. **Roteiro de Ingestão e Rollback (Mês de Teste — Junho/2025):**
   - No topo direito do Dashboard, alterne o seletor de mês de `Julho 2025` para **`Junho 2025`**.
   - Abra o menu lateral **Entrada de Dados** e clique em **`CSV DEMO (30 LINHAS)`** para baixar um lote real de Candeias-BA.
   - Anexe o arquivo baixado e clique em **`IMPORTAR DADOS`**: veja o Firewall reter **2 batidas duplicadas (R$ 14,00 de Glosa Evitada)** e consolidar as **28 refeições válidas** instantaneamente.
   - Quer testar a reversão? Volte em **Entrada de Dados** e clique no ícone da **Lixeira Vermelha** para executar o **Rollback em 1 clique**.
3. **Modo Spotlight (`📈 VER RAMPA`):** Na coluna direita (*Faturamento Detalhado*), clique em **`📈 VER RAMPA`** em qualquer empresa para isolar sua curva horária, recalcular o gargalo por minuto (`p/min`), filtrar seus adicionais/glosas e visualizar o Total Líquido exclusivo daquela entidade.
4. **Exportação Tripla Auditada:** Acesse a **Central de Relatórios** para emitir o **Boletim Executivo em PDF** (com selo criptográfico SHA-256 salvo no Cofre), o **Pacote `.ZIP` de Faturas Individuais**, a **Planilha Executiva `.XLSX` (3 Abas estilizadas)** ou o **Laudo Nominal de Duplicidades (PDF)**.

## 👨‍💻 Autor

**Ricardo Silva Lima**  
*Gestão de Processos & Conformidade B2B | Otimização Operacional | Graduando em Administração*  

📍 Salvador, Bahia, Brasil  

> *"Focado em automação, eficiência B2B e democratização do impacto social através da tecnologia."*

[![LinkedIn](https://img.shields.io/badge/LinkedIn-0077B5?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/ricardo-lima-a29240225/)
[![Email](https://img.shields.io/badge/Email-D14836?style=for-the-badge&logo=gmail&logoColor=white)](mailto:ricardosilvax86@gmail.com)
[![WhatsApp](https://img.shields.io/badge/WhatsApp-25D366?style=for-the-badge&logo=whatsapp&logoColor=white)](https://wa.me/5571986030162)
  <a href="https://raw.githubusercontent.com/gestaointeligente-ia/refeitorio/main/curr%C3%ADculo_Ricardo_Lima-rev10" download="Curriculo_Ricardo_Lima.pdf" target="_blank">
  <img src="https://img.shields.io/badge/CURR%C3%8DCULO-PDF-E63946?style=for-the-badge&logo=adobe-acrobat-reader&logoColor=white&labelColor=343A40" alt="Descarregar Currículo" />
</a>
