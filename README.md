# 🤖 AI Pulse — Sistema de Agregação de Notícias de IA
 
> Projeto desenvolvido para o Processo Seletivo do **Inteli Academy**.  
> Automação inteligente com n8n + Gemini AI para curadoria semanal de notícias de Inteligência Artificial.
 
---
 
## 📌 Sobre o Projeto
 
O **AI Pulse** é uma plataforma de curadoria automatizada de notícias sobre Inteligência Artificial. O sistema coleta notícias de múltiplas fontes RSS, filtra e consolida o conteúdo usando IA (Google Gemini), e entrega um resumo curado via site interativo e newsletter multicanal (Email, Slack e Telegram).
 
O projeto resolve o problema da **fragmentação informacional** no mundo da IA — centralizando, filtrando e resumindo o que realmente importa para a comunidade do Inteli Academy.
 
---
 
## 🎯 Objetivo
 
Desenvolver um workflow no n8n capaz de:
 
- Escanear múltiplas fontes RSS de notícias de IA
- Filtrar e remover duplicatas automaticamente
- Usar IA generativa (Gemini) para curadoria editorial
- Entregar as notícias em um site interativo com gamificação
- Enviar newsletter automatizada por Email, Slack e Telegram
 
---
 
## 🏗️ Arquitetura do Sistema
 
```
Webhook / Schedule Trigger
        ↓
RSS Read (9 fontes simultâneas)
        ↓
Merge (consolidação em árvore)
        ↓
Code - Padroniza e Resume
        ↓
Code - Remove Duplicados
        ↓
Code - Filtro de Notícias
        ↓
Code - AI Token Control
        ↓
Code - Prompt AI
        ↓
AI Agent (Google Gemini)
        ↓
Code - Formata Saída
        ↓
Respond to Webhook → Site HTML
        ↓
Newsletter (Email + Slack + Telegram)
```
 
---
 
## 🔧 Tecnologias Utilizadas
 
| Tecnologia | Uso |
|---|---|
| **n8n** | Plataforma de automação e orquestração do workflow |
| **Google Gemini** | Modelo de IA para curadoria e geração de resumos |
| **RSS Feed** | Coleta de notícias de múltiplas fontes |
| **HTML / CSS / JS** | Frontend interativo do site AI Pulse |
| **GitHub Pages** | Hospedagem do site |
| **n8n Cloud** | Hospedagem do workflow em produção |
 
---
 
## 📡 Fontes de Dados (RSS)
 
O sistema coleta notícias simultaneamente de 9 fontes:
 
- TechCrunch AI
- VentureBeat AI
- The Verge
- Wired
- MIT Technology Review
- Google News (IA)
- The Next Web
- O'Reilly Radar
- Outras fontes relevantes de IA
 
---
 
## 🧠 Como Funciona o Workflow
 
### 1. Coleta (RSS Read)
Nove nós RSS coletam artigos em paralelo, conectados em uma árvore de Merge para consolidar todos os itens.
 
### 2. Padronização
O nó `Code - Padroniza e Resume` normaliza os campos de cada notícia (título, fonte, link, data, resumo) para um formato único.
 
### 3. Remoção de Duplicatas
O nó `Code - Remove Duplicados` compara títulos e links para eliminar conteúdo repetido.
 
### 4. Filtro de Relevância
O nó `Code - Filtro de Notícias` remove conteúdo promocional, webinars, podcasts e posts sem impacto real.
 
### 5. Controle de Tokens
O nó `Code - AI Token Control` limita a quantidade de notícias enviadas para a IA, evitando exceder o contexto do modelo.
 
### 6. Curadoria com IA
O `Code - Prompt AI` monta o prompt editorial e o `AI Agent` (Gemini) seleciona as 6 notícias mais relevantes, gerando:
- Título refinado
- Resumo editorial
- Categoria
- Score de relevância (0-10)
- Nível de impacto
- "Why it matters"
- Tags
 
### 7. Entrega
O `Code - Formata Saída` estrutura o JSON final e o `Respond to Webhook` devolve para o site. Paralelamente, a newsletter é enviada por Email, Slack e Telegram.
 
---
 
## 🌐 Site — AI Pulse Frontend
 
O site foi desenvolvido em HTML/CSS/JS puro com:
 
- **Busca de notícias** via chamada ao webhook do n8n
- **Filtro por categoria** (IA Generativa, Aprendizado de Máquina, Ética em IA, etc.)
- **Busca por título**
- **Sistema de gamificação** — pontuação e níveis por notícias lidas
- **Newsletter resumo** exibida no topo
- **Modo demo local** como fallback
- **Design responsivo** dark mode
 
### Acesso
🔗 [Site no GitHub Pages](https://SEU-USUARIO.github.io/SEU-REPO)
 
---
 
## 🚀 Como Executar Localmente
 
### Pré-requisitos
- [n8n](https://n8n.io) instalado (via npm, Docker ou n8n Cloud)
- Chave de API do Google Gemini
 
### Passos
 
**1. Clonar o repositório**
```bash
git clone https://github.com/SEU-USUARIO/SEU-REPO.git
cd SEU-REPO
```
 
**2. Subir o n8n localmente**
```bash
docker run -it --rm \
  --name n8n \
  -p 5678:5678 \
  -v ~/.n8n:/home/node/.n8n \
  n8nio/n8n
```
 
**3. Importar o workflow**
- Acesse `http://localhost:5678`
- Vá em **Settings → Import workflow**
- Selecione o arquivo `workflow.json`
- Configure a credencial do Google Gemini
- Ative o workflow (toggle verde)
 
**4. Rodar o site**
```bash
python3 -m http.server 3000
```
Acesse `http://localhost:3000`
 
**5. Testar**
Clique em **"Buscar notícias via n8n"** no site.
 
---
 
## ☁️ Deploy em Produção
 
### n8n Cloud
1. Crie conta em [n8n.io](https://n8n.io)
2. Importe o `workflow.json`
3. Configure as credenciais (Gemini, Gmail, Slack, Telegram)
4. Ative o workflow
5. Copie a **Production URL** do nó Webhook
 
### GitHub Pages
1. Atualize `N8N_WEBHOOK_URL` no `index.html` com a URL do n8n Cloud
2. Faça push para o repositório
3. Ative GitHub Pages em **Settings → Pages → main branch**
 
---
 
## 📬 Newsletter Multicanal
 
O sistema envia automaticamente o resumo curado por três canais:
 
| Canal | Tecnologia |
|---|---|
| 📧 Email | Gmail via n8n + SMTP |
| 💬 Slack | Slack Bot via n8n |
| 📱 Telegram | Telegram Bot via n8n |
 
---
 
## 🎮 Gamificação
 
O site possui um sistema de pontuação para engajamento:
 
| Ação | Pontos |
|---|---|
| Marcar notícia como lida | +10 pts |
| A cada 50 pontos | Sobe 1 nível |
 
---
 
## 📁 Estrutura do Repositório
 
```
├── index.html          # Frontend do site AI Pulse
├── workflow.json       # Workflow do n8n (exportado)
└── README.md           # Este arquivo
```
 
---
 
## 🧪 Critérios de Criatividade Implementados
 
- ✅ **Sistema de gamificação** — pontuação e níveis por engajamento
- ✅ **Newsletter multicanal** — Email, Slack e Telegram automatizados
- ✅ **Score de relevância e impacto** — cada notícia tem score 0-10 e nível de impacto
- ✅ **"Why it matters"** — análise editorial do Gemini explicando a importância de cada notícia
- ✅ **Deduplicação automática** — sistema inteligente de remoção de duplicatas
- ✅ **Controle de tokens** — gerenciamento eficiente do contexto da IA
 
---
 
## 👤 Autor
 
**Bruno** — Candidato ao Processo Seletivo Inteli Academy  
Entrega: 05 de Abril de 2026