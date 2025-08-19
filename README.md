# AgenteMCP
Aplicação Airbnb do conceito MCP em n8n


📂 Fluxo 1 – mcp testes.json
👉 Esse fluxo é um laboratório de integrações MCP no n8n.

Ele cria vários AI Agents (todos com GPT-4o-mini) conectados a diferentes MCP Servers.
O que cada parte faz:

Brave Search (listar e executar) → Permite que o agente consulte notícias/informações atualizadas da web.
Apify (listar e executar) → Acessa scrapers/atores da Apify para automações de coleta de dados.
Airbnb (listar e executar) → Conecta ao MCP server do Airbnb para buscar hospedagens, reviews ou dados de acomodações.
21st Dev (listar e executar) → Provavelmente integrado a APIs/dev tools (parece ser algo ligado a design/frontend).
DeepSeek, Discord, etc. → Também aparecem como integrações opcionais, para IA de pesquisa, comunidade ou extração de dados.

📌 Resumindo: esse fluxo é um playground multi-ferramentas, testando como cada MCP Server pode ser consumido por agentes no n8n.

📂 Fluxo 2 – agente com mcp server.json

👉 Esse é mais focado e finalizado, com nome:
“Assistente Full – Pesquisas Brave e Airbnb”

O que ele faz:

Entrada de pesquisa (via chat ou outro workflow).
Seta a query (setarPesquisa) e envia para o AI Agent.
O AI Agent (GPT-4o-mini) tem um prompt específico:
Se for tema de internet → divide em 3 tópicos de pesquisa e busca as 3 notícias mais relevantes via Brave Search.
Se for sobre hospedagens → busca as 3 melhores acomodações no Airbnb.
Para isso, ele usa os nós:
airbnbListTools + airbnbExecuteTools
braveSearchListTools + braveExecuteListTools
O output é devolvido em JSON estruturado com:

{
  "item_1": "resultado 1",
  "item_2": "resultado 2",
  "item_3": "resultado 3"
}


📌 Resumindo: esse fluxo é um assistente de pesquisa dual → Web (Brave) + Hospedagens (Airbnb). Ele pega uma entrada aberta do usuário e transforma em resultados prontos para análise.
