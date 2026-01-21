Agente de Gastos – Bot Financeiro com n8n + Supabase

O Agente de Gastos é um bot inteligente criado no n8n usando LangChain + OpenAI, integrado ao Supabase, que permite:

 Visualizar gastos

 Adicionar novos gastos

 Editar gastos existentes

 (Opcional) Deletar gastos

Tudo por meio de conversa em linguagem natural.

 Como funciona

O fluxo é acionado sempre que uma mensagem é recebida no chat.
O agente interpreta a intenção do usuário e chama automaticamente a tool correta no Supabase.

Arquitetura
Usuário
   ↓
Chat Trigger (n8n)
   ↓
AI Agent (LangChain + GPT)
   ↓
Supabase Tools
   ↓
Tabela: gastos

 Estrutura da Tabela no Supabase

Tabela: gastos

Campo	Tipo	Descrição
nome	text	Nome do gasto
valor	number	Valor do gasto
tipo	text	Categoria do gasto
Categorias possíveis

O agente classifica automaticamente em apenas 4 tipos:

Supermercado

Diversão

Saúde

Educação

 Tools configuradas
Tool	Ação	Descrição
tool_visualizar_gastos	GET	Lista todos os gastos
tool_criar_gasto	INSERT	Cria um novo gasto
tool_atualizar_gasto	UPDATE	Atualiza um gasto
tool_deletar_gasto	DELETE	Remove um gasto
 Regras do Agente

O sistema segue estas instruções:

1️ Visualizar gastos

“Quero ver meus gastos”
“Mostre os gastos do mês”

O bot:

Lista nome, tipo e valor

Se necessário, pede filtro (tipo ou período)

2️ Adicionar gasto

Exemplo:

“Gastei 120 reais no mercado”

O agente extrai:

nome_gasto

valor_gasto

tipo_gasto (classificado automaticamente)

Antes de salvar, ele confirma com o usuário.

3️ Editar gasto

Fluxo:

Pergunta qual gasto editar

Mostra os gastos para confirmar

Confirma o nome exato

Atualiza no Supabase

Exibe o resultado

 Tecnologias

n8n

LangChain Agent

OpenAI (gpt-4.1-mini)

Supabase

Memory Buffer Window

 Como usar

Importe o arquivo Agente de gastos.json no n8n

Configure:

Credenciais do OpenAI

Credenciais do Supabase

Crie a tabela gastos

Ative o workflow

Envie mensagens pelo Chat Trigger 

Exemplos de comandos

“Adicionar gasto de 50 no cinema”

“Quero ver meus gastos”

“Editar gasto do supermercado”

“Trocar valor do gasto da faculdade”
