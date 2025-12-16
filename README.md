# AgenteMCP  
Aplicação do conceito **MCP (Model Context Protocol)** utilizando **n8n**, com foco em agentes de IA conectados a múltiplos MCP Servers — incluindo **Airbnb**, **Brave Search** e outras ferramentas externas.

O projeto demonstra como orquestrar **AI Agents multi-ferramenta**, capazes de decidir dinamicamente qual MCP Server utilizar com base na intenção do usuário.

---

## 🎯 Objetivo do Projeto

Demonstrar, de forma prática e funcional, como o conceito de **MCP** pode ser aplicado no n8n para:

- Criar agentes de IA conectados a múltiplas ferramentas externas  
- Centralizar contexto, decisão e execução em um único agente  
- Construir fluxos reutilizáveis, extensíveis e orientados a intenção  
- Simular um ambiente real de **AI Tooling Orchestration**

---

## 🧠 Conceito Central

Em vez de hardcodar integrações, o agente:

- Recebe uma intenção aberta do usuário  
- Interpreta o contexto  
- Seleciona dinamicamente o MCP Server adequado  
- Executa a ação  
- Retorna um output estruturado

👉 **O agente decide a ferramenta, não o fluxo.**

---

## 📂 Fluxo 1 – `mcp testes.json`

### 🔬 Laboratório MCP (Playground)

Esse fluxo funciona como um **ambiente de testes** para integrações MCP no n8n.

### O que ele faz:
- Cria múltiplos **AI Agents** (todos com `GPT-4o-mini`)
- Conecta cada agente a diferentes **MCP Servers**
- Testa listagem de ferramentas (`list tools`)
- Testa execução real (`execute tools`)

### MCP Servers integrados:

- **Brave Search**
  - Consulta notícias e informações atualizadas da web
- **Apify**
  - Acesso a scrapers e atores para coleta automatizada de dados
- **Airbnb**
  - Busca de hospedagens, reviews e dados de acomodações
- **21st Dev**
  - Integração com ferramentas voltadas a desenvolvimento/design
- **Outros**
  - DeepSeek, Discord e integrações adicionais experimentais

📌 **Resumo:**  
Esse fluxo é um **playground multi-ferramentas**, validando como diferentes MCP Servers podem ser consumidos por agentes dentro do n8n.

---

## 📂 Fluxo 2 – `agente com mcp server.json`

### 🤖 Assistente Final:  
**“Assistente Full – Pesquisas Brave e Airbnb”**

Esse é o fluxo **mais refinado e pronto para uso**, focado em um agente com comportamento claro e objetivo.

---

### 🔁 Funcionamento do Fluxo

1. O usuário envia uma entrada de pesquisa (chat ou workflow).
2. O fluxo define a query (`setarPesquisa`).
3. A query é enviada para o **AI Agent (GPT-4o-mini)**.
4. O agente decide qual MCP Server usar com base no contexto.

---

### 🧠 Lógica do Agente

O prompt do agente define:

- **Se o tema for internet / notícias:**
  - Divide o assunto em 3 tópicos
  - Busca as 3 notícias mais relevantes via **Brave Search**

- **Se o tema for hospedagem / viagem:**
  - Busca as 3 melhores acomodações via **Airbnb**

---

### 🔧 MCP Tools Utilizadas

**Airbnb**
- `airbnbListTools`
- `airbnbExecuteTools`

**Brave Search**
- `braveSearchListTools`
- `braveExecuteListTools`

---

### 📤 Output Estruturado

O agente retorna um JSON padronizado:

```json
{
  "item_1": "resultado 1",
  "item_2": "resultado 2",
  "item_3": "resultado 3"
}

Esse formato facilita:
Consumo por outros fluxos
Persistência em banco
Geração de relatórios
Integração com dashboards ou APIs

🧩 Arquitetura Conceitual
[ Usuário ]
     |
     v
[ AI Agent ]
     |
     |—— decide contexto
     |
     +—— Brave MCP ——> Notícias / Web
     |
     +—— Airbnb MCP —> Hospedagens
     |
     v
[ Output JSON Estruturado ]

🚀 Por que esse projeto é relevante

Demonstra uso real de MCP, não apenas conceito

Mostra orquestração inteligente de ferramentas

Agente decide qual API usar, não o desenvolvedor

Arquitetura extensível para novos MCP Servers

Integra IA + automação + ferramentas externas

🧠 Conclusão
Este projeto mostra como MCP + n8n + AI Agents podem ser usados para construir assistentes realmente inteligentes, capazes de:
Entender intenção
Escolher ferramentas
Executar ações
Retornar dados estruturados
